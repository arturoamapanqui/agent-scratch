### Ejecucion de Test

❯ uv run pytest
tests/application/test_chat_service.py ........... [ 12%]
tests/application/test_chunker.py ..... [ 18%]
tests/application/test_evaluation.py ...... [ 25%]
tests/application/test_ingest_corpus.py .. [ 27%]
tests/application/test_redaction.py .. [ 30%]
tests/domain/test_golden_case.py . [ 31%]
tests/domain/test_models.py ....... [ 39%]
tests/infrastructure/test_api.py .................. [ 60%]
tests/infrastructure/test_azure_search_knowledge_base.py . [ 61%]
tests/infrastructure/test_decision_judge.py ... [ 65%]
tests/infrastructure/test_foundry_chat_model.py . [ 66%]
tests/infrastructure/test_geval_judge.py . [ 67%]
tests/infrastructure/test_golden_sets.py ....... [ 75%]
tests/infrastructure/test_health.py .. [ 77%]
tests/infrastructure/test_hybrid.py ... [ 81%]
tests/infrastructure/test_loaders.py ....... [ 89%]
tests/infrastructure/test_qdrant_knowledge_base.py .... [ 94%]
tests/infrastructure/test_settings.py ..... [100%]

======================================================== 86 passed in 0.93s ========================================================

uv run eval python .venv
INFO agent.infrastructure.bootstrap: Foundry auth provider: entra_id
INFO azure.identity.\_credentials.environment: No environment configuration found.
INFO azure.identity.\_credentials.managed_identity: ManagedIdentityCredential will use IMDS
INFO agent.infrastructure.bootstrap: Foundry auth provider: entra_id
INFO azure.identity.\_credentials.environment: No environment configuration found.
INFO azure.identity.\_credentials.managed_identity: ManagedIdentityCredential will use IMDS
INFO agent.infrastructure.bootstrap: Knowledge base: local · /Users/joseph/CodeMe/credicorp/team-5/data/index/support · 28 chunks
INFO agent.infrastructure.bootstrap: Foundry auth provider: entra_id
INFO azure.identity.\_credentials.environment: No environment configuration found.
INFO azure.identity.\_credentials.managed_identity: ManagedIdentityCredential will use IMDS
caso tipo recall intención fuentes hechos apoyo relevancia cita datos personales
INFO azure.core.pipeline.policies.http_logging_policy: Request URL: 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=REDACTED'
Request method: 'GET'
Request headers:
'x-ms-client-request-id': 'dbd84abe-deac-11f1-a3bb-09edef09b6ef'
'User-Agent': 'azsdk-python-identity/1.26.0 Python/3.12.7 (macOS-27.2.1-arm64-arm-64bit)'
No body was attached to the request
INFO azure.identity.\_credentials.chained: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO azure.core.pipeline.policies.http_logging_policy: Request URL: 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=REDACTED'
Request method: 'GET'
Request headers:
'x-ms-client-request-id': 'dd268908-deac-11f1-a3bb-09edef09b6ef'
'User-Agent': 'azsdk-python-identity/1.26.0 Python/3.12.7 (macOS-27.2.1-arm64-arm-64bit)'
No body was attached to the request
INFO azure.identity.\_credentials.chained: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6193, 'prompt_tokens': 709, 'completion_tokens': 554}
INFO azure.core.pipeline.policies.http_logging_policy: Request URL: 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=REDACTED'
Request method: 'GET'
Request headers:
'x-ms-client-request-id': 'e0d58f9a-deac-11f1-a3bb-09edef09b6ef'
'User-Agent': 'azsdk-python-identity/1.26.0 Python/3.12.7 (macOS-27.2.1-arm64-arm-64bit)'
No body was attached to the request
INFO azure.identity.\_credentials.chained: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6016, 'prompt_tokens': 752, 'completion_tokens': 619}
support-01 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5127, 'prompt_tokens': 757, 'completion_tokens': 312}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6545, 'prompt_tokens': 749, 'completion_tokens': 487}
support-02 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3938, 'prompt_tokens': 765, 'completion_tokens': 314}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4078, 'prompt_tokens': 760, 'completion_tokens': 422}
support-03 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4529, 'prompt_tokens': 726, 'completion_tokens': 367}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3951, 'prompt_tokens': 707, 'completion_tokens': 218}
support-04 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3256, 'prompt_tokens': 732, 'completion_tokens': 246}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4727, 'prompt_tokens': 720, 'completion_tokens': 423}
support-05 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3726, 'prompt_tokens': 736, 'completion_tokens': 304}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4781, 'prompt_tokens': 721, 'completion_tokens': 485}
support-06 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4496, 'prompt_tokens': 770, 'completion_tokens': 295}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3919, 'prompt_tokens': 744, 'completion_tokens': 271}
support-07 answerable ok ok ok NO 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 7689, 'prompt_tokens': 765, 'completion_tokens': 855}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5706, 'prompt_tokens': 788, 'completion_tokens': 435}
support-08 answerable ok NO ok NO 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5102, 'prompt_tokens': 748, 'completion_tokens': 541}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6926, 'prompt_tokens': 782, 'completion_tokens': 630}
support-09 answerable ok NO ok NO 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4249, 'prompt_tokens': 664, 'completion_tokens': 305}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3858, 'prompt_tokens': 646, 'completion_tokens': 332}
support-10 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 2499, 'prompt_tokens': 708, 'completion_tokens': 233}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 10066, 'prompt_tokens': 686, 'completion_tokens': 437}
support-11 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4021, 'prompt_tokens': 742, 'completion_tokens': 250}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5263, 'prompt_tokens': 735, 'completion_tokens': 416}
support-12 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3680, 'prompt_tokens': 711, 'completion_tokens': 304}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6455, 'prompt_tokens': 694, 'completion_tokens': 405}
support-13 answerable ok ok ok NO 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4179, 'prompt_tokens': 693, 'completion_tokens': 310}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3807, 'prompt_tokens': 682, 'completion_tokens': 348}
support-14 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4627, 'prompt_tokens': 741, 'completion_tokens': 486}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 7258, 'prompt_tokens': 713, 'completion_tokens': 488}
support-15 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 10423, 'prompt_tokens': 751, 'completion_tokens': 437}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4158, 'prompt_tokens': 739, 'completion_tokens': 302}
support-16 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4032, 'prompt_tokens': 695, 'completion_tokens': 360}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3201, 'prompt_tokens': 670, 'completion_tokens': 229}
support-17 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO azure.identity.\_internal.decorators: AzureCliCredential.get_token_info succeeded
INFO azure.identity.\_credentials.default: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO azure.identity.\_internal.decorators: AzureCliCredential.get_token_info succeeded
INFO azure.identity.\_credentials.default: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 10467, 'prompt_tokens': 758, 'completion_tokens': 809}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 8924, 'prompt_tokens': 810, 'completion_tokens': 967}
support-18 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5045, 'prompt_tokens': 711, 'completion_tokens': 467}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm SearchQuery {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4014, 'prompt_tokens': 225, 'completion_tokens': 362}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5557, 'prompt_tokens': 799, 'completion_tokens': 517}
INFO azure.identity.\_internal.decorators: AzureCliCredential.get_token_info succeeded
INFO azure.identity.\_credentials.default: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5579, 'prompt_tokens': 723, 'completion_tokens': 414}
support-19 follow_up ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6395, 'prompt_tokens': 726, 'completion_tokens': 429}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm SearchQuery {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5356, 'prompt_tokens': 189, 'completion_tokens': 558}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3851, 'prompt_tokens': 784, 'completion_tokens': 293}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5616, 'prompt_tokens': 710, 'completion_tokens': 404}
support-20 follow_up ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3649, 'prompt_tokens': 770, 'completion_tokens': 231}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm SearchQuery {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3480, 'prompt_tokens': 179, 'completion_tokens': 297}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 8422, 'prompt_tokens': 779, 'completion_tokens': 994}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6245, 'prompt_tokens': 781, 'completion_tokens': 700}
support-21 follow_up NO ok NO NO 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5172, 'prompt_tokens': 751, 'completion_tokens': 449}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5771, 'prompt_tokens': 750, 'completion_tokens': 567}
support-22 expired ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5409, 'prompt_tokens': 741, 'completion_tokens': 504}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5284, 'prompt_tokens': 734, 'completion_tokens': 499}
support-23 expired ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5601, 'prompt_tokens': 759, 'completion_tokens': 512}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 10387, 'prompt_tokens': 757, 'completion_tokens': 1227}
support-24 expired ok ok NO NO 5.0 5.0 0.8 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4018, 'prompt_tokens': 752, 'completion_tokens': 234}
support-25 noise - NO NO - - - - ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5973, 'prompt_tokens': 744, 'completion_tokens': 645}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 7339, 'prompt_tokens': 750, 'completion_tokens': 631}
support-26 noise ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4812, 'prompt_tokens': 737, 'completion_tokens': 401}
support-27 out_of_scope - ok NO - - - - ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3046, 'prompt_tokens': 747, 'completion_tokens': 257}
support-28 out_of_scope - ok ok - - - - ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3989, 'prompt_tokens': 735, 'completion_tokens': 426}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4384, 'prompt_tokens': 711, 'completion_tokens': 344}
support-29 personal_data ok NO ok NO 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4366, 'prompt_tokens': 757, 'completion_tokens': 227}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm GEvalScores {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5772, 'prompt_tokens': 726, 'completion_tokens': 353}
support-30 personal_data ok NO ok NO 5.0 5.0 1.0 ok

Resumen de 30 casos (juez local):
recall@5: 0.96 intención: 0.83 fuentes: 0.87 hechos: 0.70
apoyo: 5.0/5 relevancia: 5.0/5 cita correcta: 1.0
fugas de datos personales: 0 citas de fuentes prohibidas: 1
tokens: 22849 de entrada, 13958 de salida
Detalle de cada caso: /Users/joseph/CodeMe/credicorp/team-5/data/eval/support-20261112-102827.json

### Comparacion de jueces

uv run eval --judge azure_evaluation python .venv

INFO agent.infrastructure.bootstrap: Foundry auth provider: entra_id
INFO azure.identity.\_credentials.environment: No environment configuration found.
INFO azure.identity.\_credentials.managed_identity: ManagedIdentityCredential will use IMDS
INFO agent.infrastructure.bootstrap: Foundry auth provider: entra_id
INFO azure.identity.\_credentials.environment: No environment configuration found.
INFO azure.identity.\_credentials.managed_identity: ManagedIdentityCredential will use IMDS
INFO agent.infrastructure.bootstrap: Knowledge base: local · /Users/joseph/CodeMe/credicorp/team-5/data/index/support · 28 chunks
INFO agent.infrastructure.bootstrap: Foundry auth provider: entra_id
INFO azure.identity.\_credentials.environment: No environment configuration found.
INFO azure.identity.\_credentials.managed_identity: ManagedIdentityCredential will use IMDS
caso tipo recall intención fuentes hechos apoyo relevancia cita datos personales
INFO azure.core.pipeline.policies.http_logging_policy: Request URL: 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=REDACTED'
Request method: 'GET'
Request headers:
'x-ms-client-request-id': '5cae1e60-deae-11f1-ba6f-2b51f3c81e97'
'User-Agent': 'azsdk-python-identity/1.26.0 Python/3.12.7 (macOS-27.2.1-arm64-arm-64bit)'
No body was attached to the request
INFO azure.identity.\_credentials.chained: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO azure.core.pipeline.policies.http_logging_policy: Request URL: 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=REDACTED'
Request method: 'GET'
Request headers:
'x-ms-client-request-id': '5df05b08-deae-11f1-ba6f-2b51f3c81e97'
'User-Agent': 'azsdk-python-identity/1.26.0 Python/3.12.7 (macOS-27.2.1-arm64-arm-64bit)'
No body was attached to the request
INFO azure.identity.\_credentials.chained: DefaultAzureCredential acquired a token from AzureCliCredential
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6794, 'prompt_tokens': 709, 'completion_tokens': 490}
INFO azure.core.pipeline.policies.http_logging_policy: Request URL: 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=REDACTED'
Request method: 'GET'
Request headers:
'x-ms-client-request-id': '61fb2ef8-deae-11f1-ba6f-2b51f3c81e97'
'User-Agent': 'azsdk-python-identity/1.26.0 Python/3.12.7 (macOS-27.2.1-arm64-arm-64bit)'
No body was attached to the request
INFO azure.identity.\_credentials.chained: DefaultAzureCredential acquired a token from AzureCliCredential
support-01 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4677, 'prompt_tokens': 757, 'completion_tokens': 252}
support-02 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4211, 'prompt_tokens': 765, 'completion_tokens': 378}
support-03 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5074, 'prompt_tokens': 726, 'completion_tokens': 441}
support-04 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4059, 'prompt_tokens': 732, 'completion_tokens': 313}
support-05 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3569, 'prompt_tokens': 736, 'completion_tokens': 310}
support-06 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3466, 'prompt_tokens': 770, 'completion_tokens': 167}
support-07 answerable ok ok ok NO 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5667, 'prompt_tokens': 765, 'completion_tokens': 468}
support-08 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 7253, 'prompt_tokens': 748, 'completion_tokens': 816}
support-09 answerable ok NO ok NO 4.8 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3420, 'prompt_tokens': 664, 'completion_tokens': 305}
support-10 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4925, 'prompt_tokens': 708, 'completion_tokens': 489}
support-11 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3768, 'prompt_tokens': 742, 'completion_tokens': 315}
support-12 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3256, 'prompt_tokens': 711, 'completion_tokens': 240}
support-13 answerable ok ok ok NO 5.0 4.9 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4661, 'prompt_tokens': 693, 'completion_tokens': 310}
support-14 answerable ok ok ok ok 5.0 4.9 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4138, 'prompt_tokens': 741, 'completion_tokens': 305}
support-15 answerable ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO openai.\_base_client: Retrying request in 0.451552 seconds (retry 1 of 2)
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 36973, 'prompt_tokens': 751, 'completion_tokens': 589}
support-16 answerable ok ok ok ok 4.8 4.8 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4106, 'prompt_tokens': 695, 'completion_tokens': 296}
support-17 answerable ok ok ok ok 5.0 4.9 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4938, 'prompt_tokens': 758, 'completion_tokens': 460}
support-18 answerable ok ok ok ok 4.9 4.9 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 9702, 'prompt_tokens': 711, 'completion_tokens': 465}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm SearchQuery {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 7177, 'prompt_tokens': 225, 'completion_tokens': 746}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4437, 'prompt_tokens': 799, 'completion_tokens': 508}
support-19 follow_up ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3242, 'prompt_tokens': 726, 'completion_tokens': 173}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm SearchQuery {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3956, 'prompt_tokens': 189, 'completion_tokens': 365}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5761, 'prompt_tokens': 784, 'completion_tokens': 432}
support-20 follow_up ok ok ok ok 5.0 4.9 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4197, 'prompt_tokens': 770, 'completion_tokens': 291}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm SearchQuery {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3774, 'prompt_tokens': 175, 'completion_tokens': 295}
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 5227, 'prompt_tokens': 780, 'completion_tokens': 464}
support-21 follow_up ok ok ok ok 4.9 4.9 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 6099, 'prompt_tokens': 751, 'completion_tokens': 385}
support-22 expired ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4116, 'prompt_tokens': 741, 'completion_tokens': 367}
support-23 expired ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 10424, 'prompt_tokens': 759, 'completion_tokens': 1035}
support-24 expired ok ok NO NO 4.9 4.3 0.9 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO openai.\_base_client: Retrying request in 0.441171 seconds (retry 1 of 2)
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 34568, 'prompt_tokens': 752, 'completion_tokens': 298}
support-25 noise - NO NO - - - - ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4902, 'prompt_tokens': 744, 'completion_tokens': 514}
support-26 noise ok ok ok ok 5.0 5.0 1.0 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 4445, 'prompt_tokens': 737, 'completion_tokens': 443}
support-27 out_of_scope - ok ok - - - - ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3496, 'prompt_tokens': 747, 'completion_tokens': 256}
support-28 out_of_scope - ok ok - - - - ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO openai.\_base_client: Retrying request in 0.480297 seconds (retry 1 of 2)
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 35139, 'prompt_tokens': 735, 'completion_tokens': 438}
support-29 personal_data ok ok ok ok 5.0 5.0 0.9 ok
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/embeddings "HTTP/1.1 200 OK"
INFO httpx2: HTTP Request: POST https://aif-workshop-jsu3.services.ai.azure.com/openai/v1/chat/completions "HTTP/1.1 200 OK"
INFO agent.infrastructure.llm.foundry_chat_model: llm AgentReply {'models': ['gpt-5-mini-2025-08-07'], 'llm_calls': 1, 'latency_ms': 3005, 'prompt_tokens': 757, 'completion_tokens': 289}
support-30 personal_data ok NO ok NO 5.0 5.0 1.0 ok

Resumen de 30 casos (juez azure_evaluation):
recall@5: 1.00 intención: 0.90 fuentes: 0.93 hechos: 0.81
apoyo: 5.0/5 relevancia: 4.9/5 cita correcta: 1.0
fugas de datos personales: 0 citas de fuentes prohibidas: 1
tokens: 22846 de entrada, 13779 de salida
