# rag-from-the-ground-up

Educational project to learn RAG , from teh ground up. 

Plan is to build up each piece by piece and learn it the hard way.

I've used RHPDS as a base. Added one more node as it's SNO.

```
# oc login ...

oc new-project rag-testing

source 0-secrets/env
oc create secret generic llama-stack-secret -n ${NAMESPACE} \
  --from-literal=INFERENCE_MODEL="$INFERENCE_MODEL" \
  --from-literal=VLLM_URL="$VLLM_URL" \
  --from-literal=VLLM_TLS_VERIFY="$VLLM_TLS_VERIFY" \
  --from-literal=VLLM_API_TOKEN="$VLLM_API_TOKEN" \
  --from-literal=VLLM_MAX_TOKENS="$VLLM_MAX_TOKENS" \
  --from-literal=EMBEDDING_MODEL="$EMBEDDING_MODEL" \
  --from-literal=EMBEDDING_PROVIDER_MODEL_ID="$EMBEDDING_PROVIDER_MODEL_ID" \
  --from-literal=VLLM_EMBEDDING_URL="$VLLM_EMBEDDING_URL" \
  --from-literal=VLLM_EMBEDDING_TLS_VERIFY="$VLLM_EMBEDDING_TLS_VERIFY" \
  --from-literal=VLLM_EMBEDDING_API_TOKEN="$VLLM_EMBEDDING_API_TOKEN" \
  --from-literal=VLLM_EMBEDDING_MAX_TOKENS="$VLLM_EMBEDDING_MAX_TOKENS"

# minio
oc apply -f 1-minio/minio.yaml 

# postgres for Llamastack
oc apply -f 2-llama-stack/postgresql.yaml

# llamastack
oc apply -f 2-llama-stack/lsd.yaml

```