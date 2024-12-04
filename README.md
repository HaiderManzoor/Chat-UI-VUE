# 🤖 Chat UI

<p align="left">
  <a href="https://vuejs.org/">
    <img src="https://img.shields.io/badge/Vue3-brightgreen.svg" alt="vue">
  </a>
  &nbsp
  <a href="https://vuetifyjs.com/">
    <img src="https://img.shields.io/badge/Vuetify-blue.svg" alt="element-ui">
  </a>
  &nbsp
  <a>
    <img src="https://img.shields.io/badge/HTML-red.svg">
  </a>
  &nbsp
  <a href="https://hub.docker.com/repository/docker/aiql/chat-ui/tags?page=1&ordering=last_updated">
    <img src="https://img.shields.io/badge/Docker-lightskyblue.svg">
  </a>
  &nbsp
  <a href="https://github.com/AI-QL/chat-ui/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/AI-QL/chat-ui" alt="license">
  </a>
</p>

The **Chat UI** project is a minimalist and efficient way to create a fully functional chatbot interface. It integrates with various backend solutions, including OpenAI, HuggingFace, and more, all with minimal setup. This repository allows for quick experimentation with chatbot functionality while maintaining simplicity.

---

## 🚀 Features

- **OpenAI-format compatibility**: Easily integrates with `HuggingFace`, `vLLM`, and more backends.
- **Multiple response formats**: Supports `OpenAI`, `Cloudflare AI`, and `plain text` responses without additional configuration.
- **Custom backend support**: Configure your own endpoints for universal chatbot usage across projects.
- **Chat history download**: Save chat history for future reference or testing.
- **Multimodal support**: Send image inputs for vision models.
- **Markdown support**: Toggle between `original format` and `Markdown` display.
- **Internationalization**: Full support for localization (`i18n`) to reach a wider audience.

---

## 📥 How to Use

#### Option 1: Goto demo [AIQL](https://chat.aiql.com/)
> The demo will use `Llama-3.2` by default, image upload is only supported for vision models

#### Option 2: Download [Index](./index.html) and open it locally (recommended)

#### Option 3: Download [Index](./index.html) and deploy it by python
```shell
cd /path/to/your/directory
python3 -m http.server 8000
```
> Then, open your browser and access `http://localhost:8000`

#### Option 4: fork this repo and link it to [Cloudflare pages](https://developers.cloudflare.com/pages)
- demo https://www2.aiql.com

#### Option 5: Deploy your own Chatbot by [Docker](https://hub.docker.com/repository/docker/aiql/chat-ui/tags?page=1&ordering=last_updated)
```shell
docker run -p 8080:8080 -d aiql/chat-ui
```

#### Option 6: Deploy within [Huggingface](https://huggingface.co/spaces/AI-QL/chat-ui)
> Don't forget add `app_port: 8080` in `README.md`

#### Option 7: Deploy within [K8s](#k8s-section)


## ⚙️ How to Configure

By default, the Chat UI uses OpenAI's API format. You can easily change the API to other vendors by configuring the API Key and Endpoint.

1. **Download the configuration template** from the example folder.
2. **Insert your own API Key** for quick configuration.

---

## 🛠️ Troubleshooting

If you're having trouble accessing the page or experiencing issues, try the following:

### 1. **Reset Interface Configuration**
- Click the `Refresh` icon in the upper-right corner of the **Interface Configuration**.

### 2. **Reset All Configuration**
- Click the hidden button on the right side of the index page.
- Click the `Reset All Config` icon.

### 3. **Clear Cache**
- Right-click on the page and open the `Network` section.
- Clear your browser's cache and cookies to ensure you're using the latest version.
- Check the browser's **Network** section to find any failing resources and see if the issue is location-specific.

---

<a id="k8s-section"></a>
## Kubernetes (K8s) Deployment

1. Introduce the image as sidecar container
```yaml
spec:
  template:
    metadata:
       labels:
         app: my-app
    spec:
      containers:
      - name: chat-ui
        image: aiql/chat-ui
        ports:
        - containerPort: 8080
```

2. Add service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: chat-ui-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 8080
  type: LoadBalancer
```

3. You can access the port or add other ingress
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1
spec:
  rules:
  - host: chat-ui.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: chat-ui-service
            port:
              number: 8080
```
---

## Demo
![demo](https://github.com/user-attachments/assets/5825a8e7-0b93-4f18-bfa2-1128b9081e80)

---

## 👤 Author

**Author**: Haider Manzoor

---
