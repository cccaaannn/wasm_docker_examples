# Go compile for wasm

---

### **Docker desktop and ubuntu wsl is used in the example.**

### 1. Enable containerd image store for docker desktop [docs.docker.com/desktop/wasm](https://docs.docker.com/desktop/wasm/)
1. Navigate to `Settings`.
2. Select the `Features in development` tab.
3. Next to `Use containerd for pulling and storing images`, select the checkbox.

### 2. Install go [go.dev/doc/install](https://go.dev/doc/install) 
1. Download
    ```shell
    wget https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
    ```
2. Remove older versions and install
    ```shell
    sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz
    ```
3. Add to path
    ```shell
    export PATH=$PATH:/usr/local/go/bin
    source ~/.bashrc
    ```

### 3. Install tinygo [tinygo.org/getting-started/install](https://tinygo.org/getting-started/install) 
1. Download
    ```shell
    wget https://github.com/tinygo-org/tinygo/releases/download/v0.29.0/tinygo_0.29.0_amd64.deb
    ```
2. Install
    ```shell
    sudo dpkg -i tinygo_0.29.0_amd64.deb
    ```

### 4. Build the project with tinygo [wasmedge.org/docs/develop/go/hello_world](https://wasmedge.org/docs/develop/go/hello_world) 
1. Build the project with [tinygo](https://tinygo.org)
    ```shell
    tinygo build -o main.wasm -target wasi main.go
    ```

### 4. Build and run Docker image for wasm [docs.docker.com/desktop/wasm](https://docs.docker.com/desktop/wasm) 
1. Build the image
    ```shell
    docker buildx build --platform wasi/wasm -t wasm-test .
    ```
2. Run the image
    ```shell
    docker run --name=wasm-test --runtime=io.containerd.wasmedge.v1 --platform=wasi/wasm wasm-test
    ```

