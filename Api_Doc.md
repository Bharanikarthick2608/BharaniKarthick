# Get Projects API Documentation
This document provides an overview of the available API endpoints for managing projects, traces, and system operations. It covers project data, trace information, and system operations.

## API Endpoints

  - [Projects](#get-projects)
  - [Project Details](#get-project-details)
  - [Project Traces](#get-project-traces)
  - [Project Evaluation](#get-project-evaluation)
  - [Analysis Trace](#get-analysis-trace)
  - [Trace Details](#get-trace-details)
  - [Health Check](#health-check)
  - [Cache Management](#cache-management)
  - [Port Configuration](#port-configuration)
  - [Server Shutdown](#server-shutdown)
  
## Base URL
The base URL for all endpoints is: `http://localhost:3000`

## API Overview
> ## **GET** `/api/projects`

## Operation Overview

This endpoint allows you to fetch all projects stored in the system. Each project contains metadata about the execution, including timing, cost, and token usage information.

## Operation Details

### Response
**Status Codes**
- `200`: Success
- `500`: Server error

#### 200 Success
A list of projects with details like ID, project name, start and end times, duration, cost, and token usage.
**Schema**
```json
[
  {
    "id": "integer",
    "project_name": "string",
    "start_time": "datetime",
    "end_time": "datetime",
    "duration": "float",
    "total_cost": "float",
    "total_tokens": "integer"
  }
]
```

**Example Response:**
```json
[
  {
    "id": 1,
    "project_name": "Document Analysis Project",
    "start_time": "2024-03-15T10:30:00",
    "end_time": "2024-03-15T10:35:00",
    "duration": 300.0,
    "total_cost": 0.15,
    "total_tokens": 1500
  }
]
```

#### 500 Internal Server Error
A server error message if something goes wrong.
**Schema**
```json
{
  "error": "string"
}
```

**Example Response:**
```json
{
  "error": "Database connection error"
}
```

## Example Usage
Python code to fetch and print all projects.

### Python
```python
import requests

def get_projects():
    response = requests.get('http://localhost:3000/api/projects')
    
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"Error: {response.json()['error']}")

# Usage
try:
    projects = get_projects()
    for project in projects:
        print(f"Project: {project['project_name']}")
        print(f"Duration: {project['duration']} seconds")
        print(f"Cost: ${project['total_cost']}")
        print("---")
except Exception as e:
    print(f"Failed to fetch projects: {str(e)}")
```
# Get Project Details 

## API Overview
> ## **GET** `/api/projects/{project_id}`


## Operation Overview

This endpoint allows you to fetch detailed information about a specific project, including all associated metadata and system information.

## Operation Details


### Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| project_id | integer | Yes | The unique identifier of the project |

### Response
**Status Codes**
- `200`: Success
- `500`: Server error
- `404`: Not Found
#### 200 Success
Returns detailed project information, including system specs like OS, Python version, CPU, GPU, and installed packages.
```json
{
  "id": "integer",
  "project_name": "string",
  "start_time": "datetime",
  "end_time": "datetime",
  "duration": "float",
  "total_cost": "float",
  "total_tokens": "integer",
  "system_info": {
    "os_name": "string",
    "os_version": "string",
    "python_version": "string",
    "cpu_info": "string",
    "gpu_info": "string",
    "disk_info": "string",
    "memory_total": "integer",
    "installed_packages": "string"
  }
}
```

**Example Response:**
```json
{
  "id": 1,
  "project_name": "Document Analysis Project",
  "start_time": "2024-03-15T10:30:00",
  "end_time": "2024-03-15T10:35:00",
  "duration": 300.0,
  "total_cost": 0.15,
  "total_tokens": 1500,
  "system_info": {
    "os_name": "Linux",
    "os_version": "Ubuntu 20.04",
    "python_version": "3.9.5",
    "cpu_info": "Intel(R) Core(TM) i7-10700K CPU @ 3.80GHz",
    "gpu_info": "NVIDIA GeForce RTX 3080",
    "disk_info": "500GB SSD",
    "memory_total": 32768,
    "installed_packages": "numpy==1.21.0,pandas==1.3.0"
  }
}
```

#### 404 Not Found
Error message if the project is not found.
**Schema**
```json
{
  "error": "string"
}
```

**Example Response:**
```json
{
  "error": "Project not found"
}
```

#### 500 Internal Server Error
Server error message.
**Schema**
```json
{
  "error": "string"
}
```

**Example Response:**

```json
{
  "error": "Database connection error"
}
```

## Example Usage
Python code to fetch and display project details for a specific project ID.
### Python
```python
import requests

def get_project_details(project_id):
    response = requests.get(f'http://localhost:3000/api/projects/{project_id}')
    
    if response.status_code == 200:
        return response.json()
    elif response.status_code == 404:
        raise Exception("Project not found")
    else:
        raise Exception(f"Error: {response.json()['error']}")

# Usage
try:
    project_id = 1
    project = get_project_details(project_id)
    print(f"Project: {project['project_name']}")
    print(f"Duration: {project['duration']} seconds")
    print(f"System: {project['system_info']['os_name']} {project['system_info']['os_version']}")
    print(f"Python Version: {project['system_info']['python_version']}")
except Exception as e:
    print(f"Failed to fetch project details: {str(e)}")
```
# Get Project Traces 

## API Overview
> ## **GET** `/api/projects/{project_id}/traces`

## Operation Overview

This endpoint allows you to fetch all execution traces for a specific project, providing summary statistics and execution details like agent calls, LLM calls, tool calls, and errors for each trace.

## Operation Details

### Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| project_id | integer | Yes | The unique identifier of the project |

### Response
### Response
**Status Codes**
- `200`: Success
- `500`: Server error

#### 200 Success
 A list of traces with details on execution times, agent/tool interactions, and errors.
```json
[
  {
    "id": "integer",
    "start_time": "datetime",
    "end_time": "datetime",
    "duration": "float",
    "total_agent_calls": "integer",
    "total_llm_calls": "integer",
    "total_tool_calls": "integer",
    "total_user_interactions": "integer",
    "total_errors": "integer"
  }
]
```

**Example Response:**
```json
[
  {
    "id": 1,
    "start_time": "2024-03-15T10:30:00",
    "end_time": "2024-03-15T10:31:00",
    "duration": 60.0,
    "total_agent_calls": 5,
    "total_llm_calls": 10,
    "total_tool_calls": 3,
    "total_user_interactions": 2,
    "total_errors": 0
  }
]
```


#### 500 Internal Server Error
Server error message
```json
{
  "error": "string"
}
```

**Example Response:**
```json
{
  "error": "Database connection error"
}
```

## Example Usage
Python code to fetch and display project traces.
### Python
```python
import requests

def get_project_traces(project_id):
    response = requests.get(f'http://localhost:3000/api/projects/{project_id}/traces')
    
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"Error: {response.json()['error']}")

# Usage
try:
    project_id = 1
    traces = get_project_traces(project_id)
    for trace in traces:
        print(f"Trace ID: {trace['id']}")
        print(f"Duration: {trace['duration']} seconds")
        print(f"Total LLM Calls: {trace['total_llm_calls']}")
        print(f"Total Tool Calls: {trace['total_tool_calls']}")
        print("---")
except Exception as e:
    print(f"Failed to fetch project traces: {str(e)}")
```

# Get Analysis Trace

## API Overview
> ## **GET** `/api/analysis_traces/{trace_id}`

## Operation Overview

This endpoint will fetch a detailed analysis of a specific trace, including calls to LLM models, tools, metrics, and system information.

## Operation Details

### Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| trace_id | integer | Yes | The unique identifier of the trace |

### Response
**Status Codes**
- `200`: Success
- `404`: Trace not found
- `500`: Server error
#### 200 Success
 Includes LLM calls, tool calls, metrics, and system information related to the trace.

```json
{
  "id": "integer",
  "project_id": "integer",
  "start_time": "datetime",
  "end_time": "datetime",
  "duration": "float",
  "llm_calls": [
    {
      "id": "integer",
      "name": "string",
      "model": "string",
      "input_prompt": "string",
      "output": "string",
      "tool_call": "string",
      "start_time": "datetime",
      "end_time": "datetime",
      "duration": "float",
      "token_usage": "integer",
      "cost": "float",
      "memory_used": "float"
    }
  ],
  "tool_calls": [
    {
      "id": "integer",
      "name": "string",
      "input_parameters": "object",
      "output": "string",
      "start_time": "datetime",
      "end_time": "datetime",
      "duration": "float",
      "memory_used": "float",
      "network_calls": "integer"
    }
  ],
  "metrics": [
    {
      "id": "integer",
      "metric_name": "string",
      "score": "float",
      "reason": "string",
      "result_detail": "object",
      "config": "object",
      "start_time": "datetime",
      "end_time": "datetime",
      "duration": "float",
      "timestamp": "datetime"
    }
  ],
  "system_info": {
    "os_name": "string",
    "os_version": "string",
    "python_version": "string",
    "cpu_info": "string",
    "gpu_info": "string",
    "disk_info": "string",
    "memory_total": "float",
    "installed_packages": "object"
  }
}
```
**Example Response:**
```
{
  "id": 123,
  "project_id": 2,
  "start_time": "2024-11-12T10:00:00Z",
  "end_time": "2024-11-12T10:30:00Z",
  "duration": 30.0,
  "llm_calls": [
    {
      "id": 1,
      "name": "Text Analysis",
      "model": "gpt-4",
      "input_prompt": "Analyze sentiment: 'Stock prices are rising.'",
      "output": "Positive",
      "start_time": "2024-11-12T10:05:00Z",
      "end_time": "2024-11-12T10:05:10Z",
      "duration": 0.17,
      "token_usage": 100,
      "cost": 0.02,
      "memory_used": 128.0
    }
  ],
  "tool_calls": [],
  "metrics": [],
  "system_info": {}
}
```
#### 404 Not Found
Error message if the trace is not found.
```json
{
  "error": "string"
}
```

**Example Response:**
```json
{
  "error": "Project not found"
}
```

#### 500 Internal Server Error
Server error message.
```json
{
  "error": "string"
}
```

**Example Response:**
```json
{
  "error": "Database connection error"
}
```

### Example Usage
Python code snippet to initiate a new trace with the specified configurations.
```
import requests

def get_analysis_trace(trace_id):
    response = requests.get(f'http://localhost:3000/api/analysis_traces/{trace_id}')
    
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"Error: {response.json()['error']}")

# Usage
try:
    trace_id = 123
    trace = get_analysis_trace(trace_id)
    print(f"Trace ID: {trace['id']}")
    print(f"Project ID: {trace['project_id']}")
    print(f"Start Time: {trace['start_time']}")
    print(f"End Time: {trace['end_time']}")
    print(f"Duration: {trace['duration']} seconds")
    print(f"LLM Calls: {len(trace['llm_calls'])}")
    for llm in trace['llm_calls']:
        print(f"  - LLM Call ID: {llm['id']}, Model: {llm['model']}, Duration: {llm['duration']} seconds")
    print("---")
except Exception as e:
    print(f"Failed to fetch analysis trace: {str(e)}")
```

# Get Trace Details

## API Overview
> ## GET `/api/traces/{trace_id}`


## Operation Overview

This endpoin returns comprehensive details about a specific trace, including all related calls and interactions.

## Operation Details

### Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| trace_id | integer | Yes | The unique identifier of the trace |


### Response
- `200`: Success
- `404`: Trace not found
- `500`: Server error
#### 200 Success
**Schema**
```json
{
  "id": "integer",
  "project_id": "integer",
  "start_time": "datetime",
  "end_time": "datetime",
  "duration": "float",
  "agent_calls": [
    {
      "id": "integer",
      "name": "string",
      "start_time": "datetime",
      "end_time": "datetime",
      "llm_calls": ["array"],
      "tool_calls": ["array"],
      "user_interactions": ["array"],
      "errors": ["array"]
    }
  ],
  "system_info": {
    "os_name": "string",
    "os_version": "string",
    "python_version": "string",
    "cpu_info": "string",
    "gpu_info": "string",
    "disk_info": "string",
    "memory_total": "float",
    "installed_packages": "object"
  }
}
```
**Example Response:**
```
{
  "id": 123,
  "project_id": 2,
  "start_time": "2024-11-12T10:00:00Z",
  "end_time": "2024-11-12T10:30:00Z",
  "duration": 30.0,
  "llm_calls": [
    {
      "id": 1,
      "name": "Text Analysis",
      "model": "gpt-4",
      "input_prompt": "Analyze sentiment: 'Stock prices are rising.'",
      "output": "Positive",
      "start_time": "2024-11-12T10:05:00Z",
      "end_time": "2024-11-12T10:05:10Z",
      "duration": 0.17,
      "token_usage": 100,
      "cost": 0.02,
      "memory_used": 128.0
    }
  ],
  "tool_calls": [],
  "metrics": [],
  "system_info": {}
}
```

### Example Usage:
Python code to fetch and display all available traces, including their statuses and creation timestamps.
```
def get_trace_details(trace_id):
    response = requests.get(f'http://localhost:3000/api/traces/{trace_id}')
    
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"Error: {response.json()['error']}")
        
# Usage
try:
    trace_id = 123
    trace = get_trace_details(trace_id)
    print(f"Trace ID: {trace['id']}, Duration: {trace['duration']}s")
    for agent in trace['agent_calls']:
        print(f"Agent Call ID: {agent['id']}, LLM Calls: {len(agent['llm_calls'])}")
except Exception as e:
    print(f"Error: {e}")
    
```

# Get Project Evaluation

## API Overview
> ## **GET** `/api/projects/{project_id}/evaluation`
## Operation Overview
This endpoint retrieves evaluation metrics for a specific project, with Trace filtering option.


## Operation Details


### Path Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| project_id | integer | Yes | The unique identifier of the project |

### Query Parameters
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| trace_id | string | No | Filter metrics by specific trace ID. Use 'all' for all traces |

### Response
- `200`: Success
- `500`: Server error


#### 200 Success
**Schema**
```json
[
  {
    "trace_id": "integer",
    "metric_name": "string",
    "score": "float",
    "reason": "string",
    "result_detail": "object",
    "config": "object",
    "start_time": "datetime",
    "end_time": "datetime",
    "duration": "float",
    "timestamp": "datetime"
  }
]
```
**Example Response :**
```
[
  {
    "trace_id": 1,
    "metric_name": "accuracy",
    "score": 0.95,
    "reason": "High accuracy achieved",
    "result_detail": {...},
    "config": {...},
    "start_time": "2024-01-01T00:00:00Z",
    "end_time": "2024-01-01T00:01:00Z",
    "duration": 60,
    "timestamp": "2024-01-01T00:01:00Z"
  }
]
```
**Example Usage**
```
import requests

def get_project_evaluation(project_id, trace_id="all"):
    url = f'http://localhost:3000/api/projects/{project_id}/evaluation'
    params = {'trace_id': trace_id}
    response = requests.get(url, params=params)
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"Error {response.status_code}: {response.text}")

try:
    project_id = 123
    evaluation_data = get_project_evaluation(project_id, trace_id="all")
    print(evaluation_data)
except Exception as e:
    print(f"API Error: {e}")
```
# System Management

# Get Health Check

## API Overview

> ## **GET** `/health`

## Operation Overview

This is a simple endpoint used to check the health and availability of the server. It is typically used for monitoring and ensuring the API is responsive.
## Operation Details

**Response**
- `"OK"`with a status code 200 to indicate that the server is healthy and operational.

### Example Usage
To return the status of the port use this pyhton code 
```
import requests

def health_check():
    url = 'http://localhost:3000/health'
    response = requests.get(url)
    if response.status_code == 200:
        return response.text
    else:
        raise Exception(f"Error {response.status_code}: {response.text}")

try:
    status = health_check()
    print(status)
except Exception as e:
    print(f"API Error: {e}")
```

## API Overview
> ## **POST** `/api/cache/clear`


## Operation Overview

This endpoint clears the server's cache storage.

## Operation Details
### Caching
- Response is cached for 600 seconds (10 minutes)
- Cache can be cleared using the /api/cache/clear endpoint

### Response
- `200`: Success
- `500`: Server error

#### 200 Success
**Schema**
```json
{
  "message": "string"
}
```
**Example Response :**
```json
{
  "message": "Cache cleared successfully"
}
```

### Example Usage:
```
import requests

def clear_cache():
    url = 'http://localhost:3000/api/cache/clear'
    response = requests.post(url)
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"Error {response.status_code}: {response.text}")

try:
    result = clear_cache()
    print(result['message'])
except Exception as e:
    print(f"API Error: {e}")

```

# Get Port

## API Overview
> ## **GET** `/api/port`


## Operation Overview
This endpoint returns the current port configuration of the server. It helps determine which port the server is running on, especially useful when there are multiple environments or when running on different servers.

## Operation Details

### Response

#### 200 Success
Returns the port number on which the server is currently running.

```json
{
  "port": "string"
}
```
**Example Response**
```json
{
  "port": "3000"
}
```
### Example Usage
```
import requests

def get_port():
    url = 'http://localhost:3000/api/port'
    response = requests.get(url)
    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"Error {response.status_code}: {response.text}")

try:
    port_info = get_port()
    print(f"Server is running on port: {port_info['port']}")
except Exception as e:
    print(f"API Error: {e}")

```
# Shutdown Server

## API Overview
> ## **POST** `/api/shutdown`

## Operation Overview
This endpoint allows for a graceful shutdown of the server. It ensures that all ongoing processes are completed before the server is stopped.

## Operation Details

### Authentication
- Only accessible from localhost (127.0.0.1, ::1, localhost)

### Response
- `200`: Success
- `403`: Forbidden (if not called from localhost)
#### 200 Success

The server will begin the shutdown process.
```json
{
  "message": "string"
}
```
**Example Response**
```json
{
  "message": "Server shutting down..."
}
```
### example Usage
```
import requests

def shutdown_server():
    url = 'http://localhost:3000/api/shutdown'
    response = requests.post(url)
    if response.status_code == 200:
        return response.json()
    elif response.status_code == 403:
        raise Exception("Forbidden: Only accessible from localhost")
    else:
        raise Exception(f"Error {response.status_code}: {response.text}")

try:
    shutdown_message = shutdown_server()
    print(shutdown_message['message'])
except Exception as e:
    print(f"API Error: {e}")

```
#### 403 Forbidden
Returned when the request is not from localhost

## Example Usage

### Python
```python
import requests

class DashboardAPI:
    def __init__(self, base_url="http://localhost:3000"):
        self.base_url = base_url

    def get_analysis_trace(self, trace_id):
        response = requests.get(f"{self.base_url}/api/analysis_traces/{trace_id}")
        if response.status_code == 200:
            return response.json()
        raise Exception(f"Error: {response.json().get('error', 'Unknown error')}")

    def get_trace(self, trace_id):
        response = requests.get(f"{self.base_url}/api/traces/{trace_id}")
        if response.status_code == 200:
            return response.json()
        raise Exception(f"Error: {response.json().get('error', 'Unknown error')}")

    def get_project_evaluation(self, project_id, trace_id=None):
        params = {"trace_id": trace_id} if trace_id else {}
        response = requests.get(
            f"{self.base_url}/api/projects/{project_id}/evaluation",
            params=params
        )
        if response.status_code == 200:
            return response.json()
        raise Exception(f"Error: {response.json().get('error', 'Unknown error')}")

    def clear_cache(self):
        response = requests.post(f"{self.base_url}/api/cache/clear")
        if response.status_code == 200:
            return response.json()
        raise Exception(f"Error: {response.json().get('error', 'Unknown error')}")

    def get_port(self):
        response = requests.get(f"{self.base_url}/api/port")
        if response.status_code == 200:
            return response.json()
        raise Exception(f"Error: {response.json().get('error', 'Unknown error')}")

# Usage Example
try:
    api = DashboardAPI()
    
    # Get analysis trace
    trace_data = api.get_analysis_trace(1)
    print(f"Trace Analysis: {trace_data}")
    
    # Get project evaluation
    evaluation_data = api.get_project_evaluation(1, trace_id="all")
    print(f"Project Evaluation: {evaluation_data}")
    
    # Clear cache
    cache_result = api.clear_cache()
    print(f"Cache Clear Result: {cache_result}")
    
except Exception as e:
    print(f"API Error: {str(e)}")
```