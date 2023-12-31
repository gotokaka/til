※notionに記録したドキュメントを貼り付けなおしたものです。実験。


# 概要

第7週講義の学習記録です。

# 内容

### 実行したこと

https://github.com/gotokaka/RaiseTechTask7

## 経過 2023年5月31日

cehckstyle関連の抜けを確認。

![スクリーンショット 2023-05-31 12.36.02.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f929043a-c5d6-4a84-997f-449c0db7eb59/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-05-31_12.36.02.png)

実行成功したが、以下のcheckstyle上の警告が出た。

![スクリーンショット 2023-05-31 12.25.44.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0dc3ee26-6658-4e5c-b432-e6050d3a09c2/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-05-31_12.25.44.png)

`import org.springframework.web.bind.annotation.*;` に関しては、使うのかどうなのか問題がある。アノテーションが多く使われると一つに統合してくれるらしい。checkstyle的には非推奨だが、一体どうなのだろうか？？？質問する。

[Javaプロジェクト規約 - コーディング規約の一例](http://www.02.246.ne.jp/~torutk/javaproject/codingrule.html)

[import文チェック](http://www.limy.org/program/java/checkstyle/imports.html)

### インポート文の自動化問題

以下に色々纏めている

https://github.com/gotokaka/RaiseTechTask7/issues/5

実際になったこと

![ano.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/82ead502-70ef-44ea-96bb-7a7b61848c3e/ano.gif)

消してやってもダメ。

参考にした記事。

[IntelliJ Ideaでインポートのワイルドカードを無効化する - Qiita](https://qiita.com/Yuki10/items/9ebb7f1bdf4c800765ac)

「**ワイルドカードのインポートを無効にする」の項を参照。**

[自動インポート  | IntelliJ IDEA ドキュメント](https://pleiades.io/help/idea/creating-and-optimizing-imports.html#disable-imports)

https://github.com/gotokaka/RaiseTechTask7/issues/5

その他全部issueに書いた

## 経過 2023年6月1日

コードに変更を書き加える

<aside>
<img src="/icons/exclamation-mark_yellow.svg" alt="/icons/exclamation-mark_yellow.svg" width="40px" /> 課題

オリジナルの仕様を加えてみましょう。
例）
http://localhost:8080/names?name=koyama のようにクエリ文字列を受け取れるようにする
名前以外にも生年月日を受け取れるよう実装する
バリデーションについて調べてnameが空文字、null、20文字以上の場合はエラーとす

</aside>

[【SpringBoot】リクエストパラメータを取得できるようにする@RequestParamアノテーションを解説します](https://www.tairaengineer-note.com/springboot-requestparam-annotation/)

クエリ文字列を受け取るにはこれかも？

### 他の受講生さんのもの

青木さんの第7回の課題を動かしてみた

https://github.com/takahiro-aoki494/raisetech-java-kadai7

`validation`　が動かない。

![スクリーンショット 2023-06-01 14.18.31.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b837b7b0-f168-41b1-a69e-5d786b119c76/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-01_14.18.31.png)

[Springでバリデーションがimportされていないときの対処法](https://loglog.xyz/programming/add_spring_validation)

[SpringBoot 2.3以降でjavax.validationのimportができない](https://dev.thanaism.com/2021/11/coding-java/)

`import javax.validation` が上手くインポートできない。build.gradleの依存関係を追加したがならない。

保留。

[Seventh-lesson/src/main/java/com/example/SeventhHomemork at main · kamide28/Seventh-lesson](https://github.com/kamide28/Seventh-lesson/tree/main/src/main/java/com/example/SeventhHomemork)

**@RequestParam**

空白だった時のためのバリデーションjavaxでインポートできない。なぜか？そのうち聞く。

回答

![スクリーンショット 2023-06-02 13.06.16.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfe331c8-504a-4567-8f40-87c54e9dae88/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-02_13.06.16.png)

![スクリーンショット 2023-06-02 13.06.52.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4a4df9f-cfad-47e1-8563-46a60d14bf06/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-02_13.06.52.png)

### 解決策と原因

## 経過 2023年6月2日

https://github.com/gotokaka/RaiseTechTask7/issues/2

### 現状

1. `@GetMapping`でGETリクエストのパラメータが空白やnullの場合に返すエラーが500になる
2. POST,PATCHに関しても、リクエストボディを記載しても、空白にしても、全て成功したことになってしまう。

### 解決策の調査

- クエリパラメータが不正の場合に500を返すのはSpring自体の仕様なので、500を返さないレスポンスボディをこちら側で準備しなければならない。講師：小山さんからのアドバイスと検索内容を確認したところ、`ExceptionHandler`クラスというエラーを制御するクラスの実装が必要（ConstraintViolationExceptionに対するExceptionHandlerを実装）。

ということで実装試してみる。

調査手順

1. 検索でヒットしたコードや他の受講生さんのコードを見てみる
2. 自分にない実装やコードの内容の調査
3. 自分のコードに落とし込んでみる

### 1.他の良さげな受講生さんのコードを見てみる

[GitHub - kamide28/Seventh-lesson at feature/seventhhomework](https://github.com/kamide28/Seventh-lesson/tree/feature/seventhhomework)

学習過程も参考になったので利用させていただいた。

小山さんの言うように、ExceptionHandlerクラスの実装を行なっていた。

- kamide28さんのcontrollerクラス
    
    ```java
    package com.example.SeventhHomemork;
    
    import jakarta.validation.constraints.NotBlank;
    import org.hibernate.validator.constraints.Range;
    import org.springframework.format.annotation.DateTimeFormat;
    import org.springframework.http.ResponseEntity;
    import org.springframework.validation.annotation.Validated;
    import org.springframework.web.bind.annotation.*;
    import org.springframework.web.util.UriComponentsBuilder;
    
    import java.net.URI;
    import java.util.Map;
    
    @RestController
    @Validated
    public class UsersController {
    
        @GetMapping("/users")
        public String users(@RequestParam("name") @NotBlank(message = "名前を入力してください") String name,
                            @RequestParam("age") @Range(max = 150, min = 0, message = "入力範囲超えています") Integer age,
                            @RequestParam("birthday") @DateTimeFormat(pattern = "yyyy/MM/dd") String birthday) {
            return "入力結果は：" + "名前" + name + "　年齢" + age + "　生年月日" + birthday + "です。";
        }
    
        @PostMapping("/users")
        public ResponseEntity<Map<String, String>> create(@RequestBody @Validated CreateForm createForm) {
            // 登録処理は省略
            URI url = UriComponentsBuilder.fromUriString("http://localhost:8080")
                    .path("/users/id") // id部分は実際に登録された際に発⾏したidを設定する
                    .build()
                    .toUri();
            return ResponseEntity.created(url).body(Map.of("message", "name successfully created"));
        }
    
        @PatchMapping("/users/{id}")
        public ResponseEntity<Map<String, String>> update(@PathVariable("id") int id, @RequestBody @Validated UpdateForm updateForm) {
            // 更新処理は省略
            return ResponseEntity.ok(Map.of("message", "name successfully updated"));
        }
    
        @DeleteMapping("/users/{id}")
        public ResponseEntity<Map<String, String>> delete(@PathVariable("id") int id) {
            return ResponseEntity.ok(Map.of("message", "name successfully deleted"));
        }
    
    }
    ```
    

### 気になったところ

- それぞれのアノテーションに対する意味や役割の理解
それぞれ調べたみた
答えに近いっぽいもの

[Spring BootのRestControllerの@PathVariableと@RequestParamの使い方や@Validate,@Validでバリデーションチェックを行う方法](https://confrage.jp/spring-bootのrestcontrollerのpathvariableとrequestparamの使い方/)

現状

https://github.com/gotokaka/RaiseTechTask7/pull/6

## 経過 2023年6月3日

昨日に続いて作業開始。今日の手順

1. コードの実行、動作確認。不具合がある部分を抽出し、それについて調べる。
2. 上記に合わせ、手掛かりになる資料を全部読んでみる（質問所での記事、受講生さんコード、GPT）
3. 書き換え手順を準備
4. 繰り返す

### 1.コードの実行、動作確認

先日ラストにpushしたコードです。https://github.com/gotokaka/RaiseTechTask7/pull/6

まずはGETリクエスト部分のみ

受講生さん、記事を参考にコードを書こうとしたが、流石にExceptionHandlerが分からなさすぎてGPTにかけた。GPTも結構適当なこと書くので、IntelliJでのエラーを確認しながらやったら落ち着いた。といった流れでできた。動くか分からんがやってみた。

コード

```java
@Validated
@RestController
public class UsersController {

  //GETリクエストをListで返すメソッド
  @GetMapping("/users")
  public String getUser(
      @RequestParam("userName")
      @NotBlank(message = "名前を入力してください") String userName,

      @RequestParam("id")
      @NotBlank
      @Pattern(regexp = "^[0-9]{3}$", message = "3桁の数字を入力してください") String id,

      @RequestParam("birthDate")
      @NotNull(message = "生年月日を入力してください")
      @DateTimeFormat(pattern = "yyyy/MM/dd")
      LocalDate birthDate) {

    return "入力情報  " + "ユーザID：" + id + " 名前：" + userName + " 生年月日：" + birthDate;
  }
```

`@ExceptionHandler` を使ったクラス

```java
package com.example.restapi;

import jakarta.validation.ConstraintViolation;
import jakarta.validation.ConstraintViolationException;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

@RestControllerAdvice
public class ValidationHandler {

  @ExceptionHandler(ConstraintViolationException.class)
  public ResponseEntity<Map<String, List<String>>> handleConstraintViolationException(
      ConstraintViolationException ex) {
    Map<String, List<String>> errors = new HashMap<>();
    for (ConstraintViolation<?> violation : ex.getConstraintViolations()) {
      String fieldName = violation.getRootBeanClass().getName().toString();
      String errorMessage = violation.getMessage();
      errors.computeIfAbsent(fieldName, key -> new ArrayList<>()).add(errorMessage);
    }
    return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(errors);
  }
}
```

正常なリクエストの場合。

![スクリーンショット 2023-06-03 13.56.05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c01c9060-f30a-4f01-8beb-c40dee30af16/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_13.56.05.png)

とりあえずOK。こうなってもらわないと困る。

次、userNameを空白にした。

![スクリーンショット 2023-06-03 13.56.36.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/276eac9f-37ac-44c7-b372-eca238490910/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_13.56.36.png)

正しい出力になった。ちゃんと400エラー出るんかい。中身分かってなくて動くの怖すぎる。読み込みします。それは後述。

次、idの空白

![スクリーンショット 2023-06-03 14.06.32.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6af8a724-46a3-4c06-951b-1d07764fd427/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_14.06.32.png)

桁数相違

![スクリーンショット 2023-06-03 14.06.47.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06cfc339-6767-434d-970a-df399b82039d/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_14.06.47.png)

ちゃんと出る。

誕生日

![スクリーンショット 2023-06-03 14.09.49.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/39e34012-8b6d-40b0-842d-707928bcdaaf/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_14.09.49.png)

Bad requestで返ってきた。これはExceptionHandlerによるものなのか？そもそも、今まで誕生日のエラーに関しての記録をしていなかったから比較が出来ない(やってもた)。

クラスごとコメントアウトして再実行かけてみた(userName,idは前回通りステータスコード500で返ってくることを確認して実行している)

![スクリーンショット 2023-06-03 14.18.01.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c1654673-ba2b-441b-8611-15d85f905ff0/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_14.18.01.png)

![スクリーンショット 2023-06-03 14.17.42.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd9d50c1-c118-412f-82e9-eed20379eb15/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_14.17.42.png)

変わらない。これはSpringが返しているものなのか？それに、`@NotNull(message = "生年月日を入力してください")`　のメッセージのカケラさえ出てこないようだ。何故か？

これも合わせて調査する。

### 調査

- エラーハンドリングとは→例外処理のこと
なので、今回出てきた500のレスポンスを400エラーとする事は正しい例外を表示する為の処理である。

[用語検索 - ZDNET Japan](https://japan.zdnet.com/glossary/exp/エラーハンドリング/?s=4#:~:text=エラーハンドリングとは、プログラム,ことが要因となる。)

- `@RestControllerAdvice` を扱うクラスについて調べた。どのコードが何を担っているのか？
-例外処理をする為のクラスを作成し、その中でそれぞれメソッドに処理したい例外を記述していくとう役割。要するに例外処理クラスという大枠であることを意味している。
- `@ExceptionHandler` このアノテーションで処理したい例外をメソッドごとに指定していく。

```java
@ExceptionHandler(ConstraintViolationException.class)//①処理したい例外
  public ResponseEntity<Map<String, List<String>>> handleConstraintViolationException(
      ConstraintViolationException ex) {
    Map<String, List<String>> errors = new HashMap<>();
    for (ConstraintViolation<?> violation : ex.getConstraintViolations()) {
      String fieldName = violation.getRootBeanClass().getName().toString();
      String errorMessage = violation.getMessage();
      errors.computeIfAbsent(fieldName, key -> new ArrayList<>()).add(errorMessage);
    }
    return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(errors);
  }
```

①処理したい例外`ConstraintViolationException.class` クラスって何？ってなるけどおそらくHTTPレスポンスボディの`"trace”` にある`jakarta.validation.ConstraintViolationException`　の部分を意味している。

それ以外がイマイチ分からない…。

[【Spring】@RestControllerAdvice を使ってREST APIのエラーハンドラを作成する | SEのプログラミングと英語の勉強ブログ](https://sebenkyo.com/2020/08/02/post-1260/)

### POST/PATCHの書き換え

![スクリーンショット 2023-06-03 16.12.31.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54e7eb3a-fd6e-4510-8ca9-f152184b0f00/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_16.12.31.png)

空文字でも200で返ってくる

表示できないかやってみた。

```java
@PostMapping("/users")
  public ResponseEntity<Map<String, String>> create(
      @RequestBody
      @NotBlank(message = "名前を入力してください")
      CreateForm createForm) {
    // 登録処理は省略
    URI url = UriComponentsBuilder.fromUriString("http://localhost:8080")
        .path("/userName/id") // id部分は実際に登録された際に発⾏したidを設定する
        .build()
        .toUri();
    return ResponseEntity.ok(Map.of("message", "name successfully created"));
  }
```

![スクリーンショット 2023-06-03 16.30.16.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/86eed669-d43c-44d6-b416-df860c27a842/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2023-06-03_16.30.16.png)

ダメ

理由

<aside>
<img src="/icons/brain_gray.svg" alt="/icons/brain_gray.svg" width="40px" /> GPT

提供されたコードにはいくつかの問題があります。

1. `@NotBlank`アノテーションの使用: `@NotBlank`アノテーションは、主に文字列のフィールドに対して使用されるべきです。しかし、`CreateForm`クラス自体に対して`@NotBlank`アノテーションが指定されています。これは不適切です。
2. バリデーション結果の返却: `@NotBlank`アノテーションによるバリデーションエラーが発生した場合、現在の実装ではエラーメッセージがクライアントに返されていません。代わりに成功した場合のメッセージのみを含む`message`フィールドが返されています。バリデーションエラーが発生した場合には、エラーメッセージを適切にクライアントに返す必要があります。

修正例として、以下のようなコードを検討してください:

```
@PostMapping("/users")
public ResponseEntity<?> create(@RequestBody @Valid CreateForm createForm, BindingResult bindingResult) {
    if (bindingResult.hasErrors()) {
        Map<String, Object> errors = new HashMap<>();
        for (FieldError error : bindingResult.getFieldErrors()) {
            errors.put(error.getField(), error.getDefaultMessage());
        }
        return ResponseEntity.badRequest().body(errors);
    }

    // 登録処理は省略

    URI url = UriComponentsBuilder.fromUriString("<http://localhost:8080>")
            .path("/userName/id") // id部分は実際に登録された際に発⾏したidを設定する
            .build()
            .toUri();

    return ResponseEntity.ok(Map.of("message", "name successfully created"));
}

```

修正点:

- `@Valid`アノテーションの追加: `@Valid`アノテーションを使用して`CreateForm`オブジェクトのバリデーションを有効化します。
- `BindingResult`の追加: `BindingResult`オブジェクトを使用してバリデーション結果を受け取ります。
- バリデーションエラー時の処理: `bindingResult.hasErrors()`を使用してバリデーションエラーの有無をチェックし、エラーメッセージを適切にクライアントに返します。バリデーションエラーがない場合は成功のレスポンスを返します。

修正後のコードでは、バリデーションエラーが発生した場合にはエラーメッセージが返されるようになります。

</aside>

`@NotBlank`　はフィールドに書かないとダメ。つまり、CreateFormクラス内に書かなきゃいけない。

それに、今のままだとさっきのキャプチャみたいにエラーが発生しても成功メッセージを返すようになる。

```java
@PostMapping("/users")
  public ResponseEntity<Map<String, String>> create(
      @RequestBody
      @Validated
      CreateForm createForm) {
    // 登録処理は省略
    URI url = UriComponentsBuilder.fromUriString("http://localhost:8080")
        .path("/userName/id") // id部分は実際に登録された際に発⾏したidを設定する
        .build()
        .toUri();
    return ResponseEntity.ok(Map.of("message", "name successfully created"));
  }
```

こちらに@Validatedを記述してクラスのバリデーションエラーを有効にする必要があった。

## 参考リンク

SpringBootに関して優しくまとめてくれている方

[SpringBoot](https://www.tairaengineer-note.com/category/program/java/springboot/)

アノテーションに関して

[よく使うSpring Boot の アノテーションまとめ - Qiita](https://qiita.com/kenny_J_7/items/79a36d14dd6c892ae430)

`@RestController`

[【Spring Boot】Controllerの基礎（REST API）](https://b1san-blog.com/post/spring/spring-controller/)

`@RequestParam`

[【SpringBoot】リクエストパラメータを取得できるようにする@RequestParamアノテーションを解説します](https://www.tairaengineer-note.com/springboot-requestparam-annotation/)

`@GetMapping`

[【SpringBoot】GETリクエストをマッピングする@GetMappingアノテーションを解説します](https://www.tairaengineer-note.com/springboot-getmapping-annotation/)

`@PostMapping`

[【SpringBoot】POSTリクエストをマッピングする@PostMappingアノテーションを解説します](https://www.tairaengineer-note.com/springboot-postmapping-annotation/)

バリデーション

[Spring BootのRestControllerの@PathVariableと@RequestParamの使い方や@Validate,@Validでバリデーションチェックを行う方法](https://confrage.jp/spring-bootのrestcontrollerのpathvariableとrequestparamの使い方/)



