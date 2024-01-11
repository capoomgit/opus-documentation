---
description: Follow up endpoint information's in the page to generate a model.
---

# ⏺ Endpoints

### Summary of workflow&#x20;

Pick any model name from **Get All Model Names** endpoint. -> Then check customizable parameters of your selection using "**Get Attributes of a Model"** endpoint. -> Use "**Create Component**" or "**Create Structure**" endpoints to generate 3D model. -> Use "**Get Job Result**" endpoint to grab download link of generated 3D model. Thats all!&#x20;

## **1. Fetching Available 3D Model Names**

## **Endpoint**: `GET /get_model_names`

To begin, you'll need to know which 3D model names are available for customization. This endpoint helps retrieve all available models categorized under "Structure" and "Component".

**Python Code**:

```python
import requests

url = "https://opus5.p.rapidapi.com/get_model_names"
headers = {
    "X-RapidAPI-Key": "YOUR_API_KEY",
    "X-RapidAPI-Host": "opus5.p.rapidapi.com"
}

response = requests.get(url, headers=headers)
model_names = response.json()
print(model_names)
```

## **2. Discovering Customizable Attributes**

### **Endpoint:** GET /get\_attributes\_with\_name

Fetch attributes for your chosen model, which include parameters like "keywords" and specific "parameters".

**Python Code:**

```url
querystring = {"name": "House"}  # Replace with your desired model name

response = requests.get(url, headers=headers, params=querystring)
model_attributes = response.json()
print(model_attributes)
```

## **3. Customize and Create 3D Models**

After deciding on the attributes, you can customize and create your 3D model.

### **a. Create Structure**

#### **Endpoint**: `POST /create_opus_structure`

**Python Code**:

```python
url = "https://opus5.p.rapidapi.com/create_opus_structure"
payload = {
    "name": "House",  
    "keywords": {
        "*": ["classic"],
        "Window": ["modern"]
    },
    "texture_resolution": "2048"
}

response = requests.post(url, json=payload, headers=headers)
created_structure = response.json()
print(created_structure)
```

### **b. Create Component**

#### **Endpoint**: `POST /create_opus_component`

Use this endpoint to create a component based on the desired attributes. Here's a Python code example to help you understand the process:

```python
import requests

url = "https://opus5.p.rapidapi.com/create_opus_component"
payload = {
    "name": "Window",
    "texture_resolution": "1024",
    "extensions": ["usd"],
    "parameters": {
        "window_outer_frame_gen/frame_width": 3,
        "window_outer_frame_gen/frame_height": 1
    }
}

headers = {
    "content-type": "application/json",
    "X-RapidAPI-Key": "YOUR_API_KEY",
    "X-RapidAPI-Host": "opus5.p.rapidapi.com"
}

response = requests.post(url, json=payload, headers=headers)
created_component = response.json()
print(created_component)
```

## **4. Checking the Job Result**

Once the model is created, you can poll for the job result using the returned UUID from the creation step.

### **Endpoint**: `GET /get_opus_job_result`

**Python Code**:

```python
import requests

url = "https://opus5.p.rapidapi.com/get_opus_job_result"
querystring = {"result_uid": "YOUR_RETURNED_UUID"}

headers = {
    "X-RapidAPI-Key": "YOUR_API_KEY",
    "X-RapidAPI-Host": "opus5.p.rapidapi.com"
}

response = requests.get(url, headers=headers, params=querystring)
job_result = response.json()
print(job_result)
```

## **5. How to Change Model Extension**

To customize your 3D model's file extension, you'll utilize the `extensions` property in the payload. The provided schema highlights several potential values:

* `usd`: Pixar's Universal Scene Description format.
* `gltf`: JSON-based 3D model format.
* `fbx`: Autodesk's Filmbox format.

For instance, if you wish to designate the model's extension to `fbx`, you would adjust the `extensions` attribute in your request payload as follows:

```python
"extensions": ["fbx"]
```

