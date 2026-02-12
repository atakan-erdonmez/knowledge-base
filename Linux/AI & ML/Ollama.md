`ollama serve` -> start ollama
`ollama pull mistral` -> pull msitral
`ollama run mistral` -> start

sudo docker run -d   -p 3000:8080   --add-host=host.docker.internal:host-gateway   -v open-webui:/app/backend/data   -e OLLAMA_IMAGES=/external  -v /custom/ollama/images:/custom/ollama/images   --name open-webui   --restart always   ghcr.io/open-webui/open-webui:main



atakan@atakan-kubuntu:~$ cat /etc/systemd/system/ollama.service
```
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/local/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"
Environment="OLLAMA_MODELS=/external"
Environment="OLLAMA_HOST=0.0.0.0:11434"
[Install]
WantedBy=default.target
```