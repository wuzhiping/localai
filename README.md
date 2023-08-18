# localai
## https://localai.io
## https://docs.flowiseai.com/chat-models/chatlocalai
## https://docs.flowiseai.com/embeddings/localai-embeddings
## https://gpt4all.io
### http://localhost:4891/v1
<pre>
git clone https://github.com/go-skynet/LocalAI
cd LocalAI
# Download gpt4all-j to models/
wget https://gpt4all.io/models/ggml-gpt4all-j.bin -O models/ggml-gpt4all-j.bin

docker run --rm --env-file .env -it -v $PWD/models:/models:cached -p 8088:8080 quay.io/go-skynet/local-ai:latest /usr/bin/local-ai

docker run --rm -ti --gpus all -p 8080:8080 -e DEBUG=true -e MODELS_PATH=/models \
       -e PRELOAD_MODELS='[{"url": "github:go-skynet/model-gallery/openllama_7b.yaml", "name": "gpt-3.5-turbo", "overrides": { "f16":true, "gpu_layers": 35, "mmap": true, "batch": 512 } } ]' \
       -e THREADS=1 \
       -v $PWD/models:/models \
       quay.io/go-skynet/local-ai:v1.23.2-cublas-cuda12  
  
# Test API
curl http://localhost:8080/v1/models
# {"object":"list","data":[{"id":"ggml-gpt4all-j.bin","object":"model"}]}
</pre>
