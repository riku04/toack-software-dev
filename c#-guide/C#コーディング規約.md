[[MSDN C# コーディング規則|https://docs.microsoft.com/ja-jp/dotnet/csharp/programming-guide/inside-a-program/coding-conventions]]に以下を加えます。

### 共通スタイル

- | 形式   | 識別子                                                       | 例                         |
  | :----- | :----------------------------------------------------------- | -------------------------- |
  | Camel  | パラメーター、ローカル変数、フィールド変数                   | option,itemName,db         |
  | Pascal | 名前空間、クラス、インターフェース、構造体、列挙型、イベント、メソッド、プロパティ、定数 | IEnumerable,GetHashCode,DB |

　２文字の場合、Camel形式はどちらも小文字、Pascal形式はどちらも大文字で表記する。

　クラスのprivateフィールド名の先頭には _ (アンダースコア)をつける。

```c#
class CamelSample
{
    private int _field;
    public void SampleFunc(int parameter)
    {
        int local;
        .....
    }
}

```

大文字 / 小文字の違いのみによる区別は避けます。  
コメント以外は半角英数のみで記述し、英単語を使用します。  
日本語名が必要な場合はコメントに含める。ローマ字綴りは禁止とします。  
スコープの短い局所変数では省略形を許可するが、それ以外では単語は省略せずに記述します。  
コレクションやリストの変数名は複数形とします。  

### アセンブリ

実行ファイルはプロジェクト名(ProjectName.exe)、DLLは名前空間およびプロジェクト名(Com.Domain.Solution.ProjectName.dll)を用います。  
DLLの名前が重複する可能性がなければ、プロジェクト名(ProjectName.dll)でもかまいません。  

実行ファイル: ProjectName.exe   
DLLファイル: Com.Domain.SolutionName.ProjectName.dll  

### ファイル

クラス名と同じ名前にします。  
基本的には1ファイルにつき1クラスですが、その他のファイルから参照していない依存度の高いクラスは、１つのファイルにまとめるか内部クラスにします。  

### プロパティ

名詞、形容詞とします。  

プロパティ: Name, Closed, Size, Position, Length  
型と同じプロパティ: public System.Drawing.Color Color { get; set; }  
論理値を返すプロパティ: Opened, Closed, Enabled, Visible, Shown  

以下に当てはまる場合はプロパティではなくメソッドを使用します。  

- 処理に時間がかかる場合
- パラメータの変更なしに異なる結果が返る場合
- ToString()などの変換を行う場合
- ToArray()などの配列が返る場合

### メソッド

動詞とします。  
インスタンスを生成するメソッドはCreate-やNew-を使います。 
論理値を返すメソッドにはIs-, Can-, Has-を使います。                 
特別な場合を除きIs+<形容詞>、Can+<動詞>、Has+<過去分詞>とします。  
型を変換するメソッドは例外的にTo-を使います。   

インスタンスを生成するメソッド: CreateInstance, NewInstance  
論理値を返すメソッド: IsNull, IsNullable, IsEmpty, CanRead, HasClosed  
型を変換するメソッド: ToString, ToInt32   

### 非同期メソッド

接尾辞として-Asyncを付けます。  

```c#
    public static async void Main()
    {
        // 非同期開始
        var task = this.ReadAsync();

        // 同期的に完了を待てます。
        await task;
    }

    // 非同期メソッドの戻り値はTask, Task<T>とします。
    public Task ReadAsync()
    {
        return Task.Run(() => this.Read());
    }
```

### パラメータ

説明的な名前をつけます。  
パラメータ名と型を見ただけで使用法が判断できるような名前が理想的です。  

メソッドパラメータ: Console.WriteLine(string message)  

※Parameters = 仮引数, Arguments = 実引数  

### ローカル変数、ループ変数

できるだけ最小のスコープ内で、使用する直前に宣言します。  
省略した名前はローカル変数以外では禁止とします。  
名前を省略した場合でも、できるだけ意味の分かる名前を付けます。  
ループ変数は

<pre>
変数名の接頭辞 + i , j
</pre>

とし、それ以上必要な場合は設計を見直します。  

```c#
for(int ci = 0;ci < clubs.size();ci++)
{
  for(int mi = 0;clubs[ci].members.size();mi++)
  {
    if(clubs[ci].members[mi] == 'Suzuki')
    // 
  }
}
```

省略形: ctor(Constructor), addr(IPAddress), conn(Connection), btn(Button)  
意味の分かる省略形: bldr, builder(StringBuilder), reader(StreamReader)  
意味の分からない省略形: sb(StringBuilder), sr(StreamReader)  
ループ変数: for(var i = 0; i < x; i++)  

### インターフェイス

Pascal形式とし、クラスの命名規則に従います。
 インターフェイスには接頭辞として`I-`をつけ、機能を定義したものには接尾辞として`-able`をつけます。

機能を定義したインターフェイス: `interface IDisposable`

インターフェイスよりも抽象クラスにできないか検討します。

### 解放が必要なオブジェクトには using を使う

IDisposableインターフェースを実装し、Dispose()メソッドが実装されているオブジェクトにはusingステートメントを使います。  
ファイル、画像、メモリ、ネットワーク、リソースを扱うオブジェクトは解放が必要となります。  

```c#
    try
    {
        string path = "test.txt";
        using (var stream = new FileStream(path, FileMode.Read))
        {
            // 処理
        }
    }
```

### 引数でコレクションを受けるときはできるだけ抽象度の高いものを使う

メソッドの引数に`IEnumerable<T>`を指定することによって、引数の内容が変化しないことを明示できます。
 `IEnumerable<T>`は"列挙可能"なことを示しますが、`IList<T>`は"追加・削除"が可能です。
 .NET 4.5以降は`IReadOnlyList<T>`もありますが、`IEnumerable<T>`の方が最初から順番にアクセスしていく意味が強いです。

```C#
    public void DoAnything(IEnumerable<T> list)
```

### Dispose() 後は null を設定する

オブジェクトは`Dispose()`後すぐにメモリから開放されるわけではありません。
 `null`を設定することにより危険な参照を避けることができます。
 実行環境によっては`null`を設定しないとガベージコレクタで解放されない場合があります。

### 引数にrefキーワードをつけたメソッドは定義しない

 理解しづらいコードになるため使用しない。

### 引数にoutキーワードをつけたメソッドは極力定義しない

outを使う場合はTryParseのみに限定し、そのほかは戻り値として返す。

### コメント 

コメントは必要最低限にし、クラス、メソッドの概要やコードから読み取れない情報などを書く。

C# ドキュメンテーション コメント形式で記述すればインテリセンス(IntelliSense)へ反映されます。  
Sandcastleなどのツールを利用すればAPIドキュメントを作成することも可能です。　　　   
VC#で///と入力すれば自動的に補完されます。　　　　　

- summary 要約です。何をするコードか1行で簡潔に記述してください。インテリセンスで表示されます。　　
- remarks 解説です。要約を補足します。　　
- param コンストラクタやメソッドのパラメータの説明を記述します。nameプロパティによりパラメータ名を指定できます。　　
- returns メソッドの戻り値の説明を記述します。結果がboolなどで説明の必要がなければ省略してもかまいません。　　

```c#
    /// <summary>
    /// MyMethodの要約です。1行で記述します。
    /// </summary>
    /// <remarks>
    /// MyMethodの補足です。
    /// 細かい内容はこちらに記述します。
    /// </remarks>
    /// <param name="x">xの説明</param>
    /// <returns>戻り値の説明</returns>
    public bool MyMethod(int x)
```

参考資料  
https://qiita.com/Ted-HM/items/67eddbe36b88bf2d441d#%E3%82%B3%E3%83%A1%E3%83%B3%E3%83%88  