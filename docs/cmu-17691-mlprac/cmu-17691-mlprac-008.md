# 08：Docker 容器化入门教程 🐳

![](img/74727bf8a578ef2ab220ae1addb35d92_1.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_2.png)

在本节课中，我们将要学习 Docker 的基础知识，并了解如何将一个机器学习模型打包成容器化的服务。我们将从 Docker 的核心概念讲起，然后通过一个具体的例子，演示如何将一个训练好的模型封装为可通过 API 访问的 Web 服务。

---

![](img/74727bf8a578ef2ab220ae1addb35d92_4.png)

## 概述：什么是 Docker 及其优势

Docker 是一种容器化技术，它允许你将应用程序及其所有依赖项打包到一个标准化的单元中，这个单元称为容器。与传统的虚拟机相比，容器更加轻量、高效和灵活。

上一节我们介绍了 Docker 的基本概念，本节中我们来看看它与虚拟机的区别以及其核心优势。

### 容器 vs. 虚拟机

虚拟机通过**虚拟机监控程序**在物理硬件上模拟出完整的操作系统环境。每个虚拟机都预先分配了固定的计算资源（如 CPU、内存、存储），这导致了资源利用缺乏灵活性。

相比之下，容器共享宿主机的操作系统内核，将应用程序及其依赖打包成一个独立的进程。容器只在需要时才动态地使用资源，就像你电脑上同时运行的多个应用程序一样，这使得资源利用效率更高。

对于机器学习应用来说，这种灵活性至关重要。你的模型服务可能在不同时间需要不同的计算资源，容器化可以确保前端应用不会因模型推理的资源消耗而变慢，同时避免在模型空闲时过度分配资源。

### Docker 的核心优势

![](img/74727bf8a578ef2ab220ae1addb35d92_6.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_8.png)

以下是使用 Docker 容器化应用的主要好处：

![](img/74727bf8a578ef2ab220ae1addb35d92_10.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_12.png)

*   **标准化**：Docker 容器提供了一致的运行时环境，确保应用在任何支持 Docker 的平台上都能以相同的方式运行。
*   **轻量级**：容器只包含运行应用所必需的组件，没有传统操作系统的冗余，因此体积更小，启动更快。
*   **可移植性**：容器解决了“在我机器上能运行”的经典问题。你可以在本地开发环境构建容器，然后轻松地将其部署到云端服务器，只要目标环境有 Docker 运行时，应用就能一致地工作。
*   **可复现性**：通过一个名为 `Dockerfile` 的声明式文件来定义如何构建容器。这确保了构建过程是可重复和可追溯的。

---

![](img/74727bf8a578ef2ab220ae1addb35d92_14.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_16.png)

## 实践：将机器学习模型容器化

![](img/74727bf8a578ef2ab220ae1addb35d92_18.png)

理解了 Docker 的优势后，我们通过一个具体项目来学习如何操作。我们将把一个基于泰坦尼克号数据集训练的随机森林模型，打包成一个可通过 HTTP API 提供预测服务的 Docker 容器。

![](img/74727bf8a578ef2ab220ae1addb35d92_20.png)

### 第一步：准备模型与 Web 服务

![](img/74727bf8a578ef2ab220ae1addb35d92_22.png)

首先，我们需要一个训练好的机器学习模型和一个简单的 Web 服务来包装它。

1.  **训练并保存模型**：我们使用 Scikit-learn 训练一个随机森林分类器，并将训练好的模型对象保存为文件（例如使用 `pickle` 库）。生成的模型文件（如 `model.pkl`）包含了所有学习到的参数。
    ```python
    import pickle
    # 假设 clf 是已训练好的模型
    with open('model.pkl', 'wb') as f:
        pickle.dump(clf, f)
    ```

2.  **创建 Flask Web 应用**：我们使用 Flask 框架创建一个简单的 Web 服务。这个服务主要提供一个 `/predict` 端点，当收到 POST 请求时，它会加载保存的模型，对传入的数据进行预测，并返回结果。
    ```python
    from flask import Flask, request, jsonify
    import pickle

    app = Flask(__name__)
    model = pickle.load(open('model.pkl', 'rb'))

    @app.route('/predict', methods=['POST'])
    def predict():
        data = request.get_json()
        prediction = model.predict([data['features']])
        return jsonify({'prediction': int(prediction[0])})

    if __name__ == '__main__':
        app.run(host='0.0.0.0', port=8080)
    ```

![](img/74727bf8a578ef2ab220ae1addb35d92_24.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_26.png)

### 第二步：编写 Dockerfile

![](img/74727bf8a578ef2ab220ae1addb35d92_28.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_30.png)

`Dockerfile` 是一个文本文件，包含了一系列指令，用于告诉 Docker 如何构建我们的容器镜像。

以下是本例的 `Dockerfile` 内容：
```dockerfile
# 使用官方的轻量级 Python 镜像作为基础
FROM python:3.8-slim

# 在容器内设置工作目录
WORKDIR /app

# 将当前目录的所有文件复制到容器的 /app 目录下
COPY . /app

# 安装 Python 依赖包
RUN pip install --no-cache-dir -r requirements.txt

# 声明容器运行时监听的端口
EXPOSE 8080

# 定义容器启动时执行的命令
CMD ["python", "app.py"]
```
其中，`requirements.txt` 文件列出了所有必需的 Python 包，例如 `flask`, `scikit-learn`, `pandas` 等。

![](img/74727bf8a578ef2ab220ae1addb35d92_32.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_34.png)

### 第三步：构建与运行容器

![](img/74727bf8a578ef2ab220ae1addb35d92_36.png)

有了 `Dockerfile` 和应用程序代码，我们就可以构建 Docker 镜像并运行容器了。

![](img/74727bf8a578ef2ab220ae1addb35d92_38.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_39.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_41.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_43.png)

1.  **构建镜像**：在包含 `Dockerfile` 的目录下执行以下命令。`-t` 参数用于给镜像命名和打标签。
    ```bash
    docker build -t ml-api:latest .
    ```

2.  **运行容器**：基于构建好的镜像启动一个容器实例。`-p` 参数将宿主机的 8080 端口映射到容器的 8080 端口，这样我们就可以从外部访问服务。
    ```bash
    docker run -p 8080:8080 ml-api:latest
    ```

![](img/74727bf8a578ef2ab220ae1addb35d92_45.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_47.png)

3.  **测试 API**：容器运行后，我们的机器学习服务就已经在后台启动了。我们可以使用 `curl` 或其他 HTTP 客户端工具来测试预测接口。
    ```bash
    curl -X POST http://localhost:8080/predict \
         -H "Content-Type: application/json" \
         -d '{"features": [1, 0, 25, 0, 0, 10]}'
    ```
    服务将返回一个 JSON 响应，包含模型的预测结果。

---

## 总结

![](img/74727bf8a578ef2ab220ae1addb35d92_49.png)

本节课中我们一起学习了 Docker 在机器学习实践中的基础应用。我们首先了解了容器化技术相较于虚拟机的优势：更高的资源利用效率和灵活性。接着，我们通过一个端到端的示例，演示了如何将一个机器学习模型（随机森林分类器）与一个轻量级 Web 框架（Flask）结合，并通过编写 `Dockerfile` 将其打包成一个独立的、可移植的容器。

![](img/74727bf8a578ef2ab220ae1addb35d92_51.png)

![](img/74727bf8a578ef2ab220ae1addb35d92_53.png)

最终，我们得到了一个封装完整的机器学习微服务。这个服务可以在任何安装了 Docker 的环境中运行，确保了开发、测试和生产环境的一致性，为集成到更大型的应用程序架构中打下了坚实的基础。在接下来的课程中，我们将探索如何使用 Docker 来构建更复杂的数据流水线和服务编排。