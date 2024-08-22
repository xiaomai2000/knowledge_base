# https://blog.csdn.net/weixin_63866037/article/details/141279919

# https://www.cnblogs.com/egalistmir/p/18347600

# https://blog.csdn.net/vivisol/article/details/140873457?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522172396410616800222835857%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=172396410616800222835857&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-140873457-null-null.142%5Ev100%5Epc_search_result_base8&utm_term=ollama%E5%BC%80%E5%90%AFembedding%20openai%E6%9C%8D%E5%8A%A1&spm=1018.2226.3001.4187


# Book:xiyouji
# curl https://www.gutenberg.org/cache/epub/23962/pg23962.txt > ./input/book.txt

"""
export OLLAMA_MODELS=/root/autodl-tmp/ollama
ollama serve

curl -fsSL https://ollama.com/install.sh | sh      
sudo ln -s /root/autodl-tmp/apps/ollama-linux-amd64 /usr/local/bin/ollama
chmod +x /root/autodl-tmp/apps/ollama-linux-amd64


配置完成后，可以开始GraphRAG的索引流程
python -m graphrag.index --root ./ragtest


For yaml config: refer：
https://github.com/TheAiSingularity/


settings.yaml

encoding_model: cl100k_base
skip_workflows: []
llm:
  api_key: ${GRAPHRAG_API_KEY}
  type: openai_chat # or azure_openai_chat
  model: mistral
  model_supports_json: true # recommended if this is available for your model.
  # max_tokens: 4000
  # request_timeout: 180.0
  api_base: http://localhost:11434/v1
  # api_version: 2024-02-15-preview
  # organization: <organization_id>
  
  
  parallelization:
  stagger: 0.3
  # num_threads: 50 # the number of threads to use for parallel processing

async_mode: threaded # or asyncio

embeddings:
  ## parallelization: override the global parallelization settings for embeddings
  async_mode: threaded # or asyncio
  llm:
    api_key: ${GRAPHRAG_API_KEY}
    type: openai_embedding # or azure_openai_embedding
    model: nomic-embed-text
    api_base: http://localhost:11434/api
    # api_version: 2024-02-15-preview
    # organization: <organization_id>
    # deployment_name: <azure_model_deployment_name>
    
    

and need to change .env file 
according to :https://blog.csdn.net/vivisol/article/details/140873457?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522172396410616800222835857%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=172396410616800222835857&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-140873457-null-null.142%5Ev100%5Epc_search_result_base8&utm_term=ollama%E5%BC%80%E5%90%AFembedding%20openai%E6%9C%8D%E5%8A%A1&spm=1018.2226.3001.4187


And then modify python file:

cp ./miniconda3/lib/python3.10/site-packages/graphrag/llm/openai/openai_embeddings_llm.py ./miniconda3/lib/python3.10/site-packages/graphrag/llm/openai/openai_embeddings_llm.py.bk.org

cp ./miniconda3/lib/python3.10/site-packages/graphrag/query/llm/oai/embedding.py ./miniconda3/lib/python3.10/site-packages/graphrag/query/llm/oai/embedding.py.bk.org

cp ./miniconda3/lib/python3.10/site-packages/graphrag/query/llm/text_utils.py ./miniconda3/lib/python3.10/site-packages/graphrag/query/llm/text_utils.py.bk.org



