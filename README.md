Sandbox SDK Python API library

Sandbox SDK Python library provides convenient access to the Sandbox SDK REST API from any Python 3.9 or newer application.
The library includes type definitions for all request parameters and response fields.
It offers both synchronous and asynchronous clients powered by httpx.
The SDK is generated with Stainless.

MCP Server

The Sandbox SDK MCP Server enables AI assistants to interact with this API.
Assistants can explore endpoints, make test requests, and use documentation to help integrate this SDK.

Note
You may need to set environment variables in your MCP client.

Documentation

The full API of this library can be found in api.md.

Installation

Install from PyPI
pip install avm_sdk

Usage

Import the client and create an instance.

Example

import os
from sandbox_sdk import SandboxSDK

client = SandboxSDK(
    api_key=os.environ.get SANDBOX_SDK_API_KEY
)

sandboxes = client.sandboxes.list()
print sandboxes.data

Async usage

Use AsyncSandboxSDK and await each API call.

Example

import os
import asyncio
from sandbox_sdk import AsyncSandboxSDK

client = AsyncSandboxSDK(
    api_key=os.environ.get SANDBOX_SDK_API_KEY
)

async def main
    sandboxes = await client.sandboxes.list
    print sandboxes.data

asyncio.run main

With aiohttp

The async client uses httpx by default.
For improved concurrency you can use aiohttp.

Install aiohttp support
pip install avm_sdk aiohttp

Enable aiohttp client

import os
import asyncio
from sandbox_sdk import DefaultAioHttpClient
from sandbox_sdk import AsyncSandboxSDK

async def main
    async with AsyncSandboxSDK(
        api_key=os.environ.get SANDBOX_SDK_API_KEY
        http_client=DefaultAioHttpClient
    ) as client
        sandboxes = await client.sandboxes.list
        print sandboxes.data

asyncio.run main

Using types

Nested request parameters are TypedDicts.
Responses are Pydantic models.

Models support
Serialize to JSON
Convert to dictionary

Nested params

Nested parameters are dictionaries.

Example

from sandbox_sdk import SandboxSDK

client = SandboxSDK

sandbox = client.sandboxes.create(
    resources={
        cpus 1
        memory 512
        storage 10
    }
)

print sandbox.resources

Handling errors

Connection errors raise APIConnectionError.
Non success responses raise APIStatusError.
All errors inherit from APIError.

Example

import sandbox_sdk
from sandbox_sdk import SandboxSDK

client = SandboxSDK

try
    client.sandboxes.list
except sandbox_sdk.APIConnectionError
    print server could not be reached
except sandbox_sdk.RateLimitError
    print rate limited
except sandbox_sdk.APIStatusError as e
    print e.status_code
    print e.response

Error codes

400 BadRequestError
401 AuthenticationError
403 PermissionDeniedError
404 NotFoundError
422 UnprocessableEntityError
429 RateLimitError
500 and above InternalServerError
Network failures APIConnectionError

Retries

Certain errors are retried twice by default.
Retryable errors include timeouts conflicts rate limits and server errors.

Configure retries

client = SandboxSDK(
    max_retries=0
)

client.with_options max_retries=5 sandboxes.list

Timeouts

Requests time out after one minute by default.

Configure timeout

client = SandboxSDK(
    timeout=20.0
)

Override per request

client.with_options timeout=5.0 sandboxes.list

Logging

Enable logging by setting environment variable
SANDBOX_SDK_LOG info
or
SANDBOX_SDK_LOG debug

Null vs missing fields

Fields may be null or missing.
Both appear as None.
Use model_fields_set to differentiate.

Accessing raw responses

Prefix with with_raw_response to access headers and raw data.

Streaming responses

Use with_streaming_response to stream response bodies.
Requires a context manager.

Custom requests

Use client.get client.post and other HTTP verbs to call undocumented endpoints.

Extra parameters

Use extra_query extra_body and extra_headers.

HTTP client configuration

Override the HTTP client to configure proxies transports or advanced behavior.

Managing HTTP resources

The client closes connections on garbage collection.
You can manually close the client or use a context manager.

Versioning

This package follows semantic versioning.
Some breaking changes may appear in minor versions if they only affect types or internals.

Determining installed version

import sandbox_sdk
print sandbox_sdk.__version__

Requirements

Python 3.9 or higher.

Contributing

See CONTRIBUTING.md for contribution guidelines.
