Sandboxes

Types

from sandbox_sdk.types import (
    Pagination,
    Sandbox,
    SandboxCreateResponse,
    SandboxListResponse,
    SandboxDeleteResponse,
    SandboxDeleteAllResponse,
    SandboxExecuteResponse,
    SandboxUploadResponse
)

Methods

POST /v1/sandboxes/create
client.sandboxes.create params
returns SandboxCreateResponse

GET /v1/sandboxes/list
client.sandboxes.list params
returns SandboxListResponse

DELETE /v1/sandboxes/id/delete
client.sandboxes.delete id params
returns SandboxDeleteResponse

DELETE /v1/sandboxes/delete-all
client.sandboxes.delete_all
returns SandboxDeleteAllResponse

GET /v1/sandboxes/id/download
client.sandboxes.download id params
returns BinaryAPIResponse

POST /v1/sandboxes/id/execute
client.sandboxes.execute id params
returns SandboxExecuteResponse

POST /v1/sandboxes/id/upload
client.sandboxes.upload id params
returns SandboxUploadResponse
