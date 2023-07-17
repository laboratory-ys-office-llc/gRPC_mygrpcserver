# Go による gRPC サーバーのサンプル

このガイドでは、Go で gRPC サーバーを設定し `grpcurl` を使用してテストする方法を説明します

## 必要なもの

- Ubuntu Linux
- Go 1.20（snap でインストール）
- Protocol Buffers コンパイラー（protoc）
- Protocol Buffers と gRPC の Go プラグイン（protoc-gen-go と protoc-gen-go-grpc）

## 手順

### サーバー起動まで

1. プロジェクト用の新しいディレクトリを作成します
   ```bash
   mkdir mygrpcserver && cd mygrpcserver
   ```
2. Go モジュールを使用してプロジェクトを初期化します
   ```bash
   go mod init github.com/yourusername/mygrpcserver
   ```
3. .proto ファイル用のディレクトリを作成します
   ```bash
   mkdir proto && cd proto
   ```
4. .proto ファイル（user.proto）を作成します
5. .proto ファイルから Go のコードを生成します
   ```bash
   protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative user.proto
   ```
6. main.go ファイルを作成します
7. gRPC サーバーを起動します
   ```bash
   go run main.go
   ```

## grpcurl でのテスト

1. grpcurl を使用して gRPC サーバーの疎通テストをします

```bash
grpcurl -d '{"name": "Your Name"}' -plaintext localhost:50051 user.UserService/GetUser
```

```json
{
  "message": "Hello Your Name"
}
```

## 参考
