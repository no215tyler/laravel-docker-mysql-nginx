## Laravel プロジェクト構築手順
0. **クローン**
    
    Laravelの環境構築するためのdocker composeの環境をクローンします
    
    ```bash
    git clone https://github.com/no215tyler/laravel-docker-mysql-nginx.git
    ```
1. **ディレクトリの移動**
    
    LaravelプロジェクトのDocker設定があるディレクトリに移動します。
    
    ```bash
    cd laravel
    ```
    
2. **Dockerコンテナのビルドと起動**
    
    Dockerイメージをビルドし、コンテナをバックグラウンドで起動します。
    
    ```bash
    docker compose build
    docker compose up -d
    ```
    
3. **Laravel プロジェクトのセットアップ**
    - **Laravel プロジェクトを作成**
        
        コンテナ内にLaravelプロジェクトを作成します。
        
        ```bash
        docker compose exec app composer create-project --prefer-dist laravel/laravel .
        ```
        
    - **アプリケーションキーの生成**
        
        Laravelのアプリケーションキーを生成して、`.env`ファイルに設定します。
        
        ```bash
        docker compose exec app php artisan key:generate
        ```
        
    - **ストレージリンクの作成**
        
        `public/storage`ディレクトリへのシンボリックリンクを作成します。
        
        ```bash
        docker compose exec app php artisan storage:link
        ```
        
    - **ディレクトリの権限設定**
        
        `storage` と `bootstrap/cache` ディレクトリに書き込み権限を設定します。
        
        ```bash
        docker compose exec app chmod -R 777 storage bootstrap/cache
        ```
        
    - **データベースのマイグレーション**
        
        データベーステーブルを作成します。
        
        ```bash
        docker compose exec app php artisan migrate
        ```
