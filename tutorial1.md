## OPUS API Tutorial: How to Customize and Fetch 3D Models

Welcome to the OPUS API tutorial. In this guide, we'll go through the process of fetching model names, obtaining attributes, customizing a 3D model, and understanding its structure using the provided JSON schema.

### **Table of Contents**
1. Fetch Model Names
2. Get Attributes of a Model
3. Customize and Create 3D Models
    * Create Structure
    * Create Component
4. Checking the Job Result
5. How to Change Model Extension

---

### **1. Fetch Model Names**

#### **Endpoint**: `GET /get_model_names`

This endpoint helps retrieve all available models categorized under "Structure" and "Component".

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

### **2. Get Attributes of a Model**
#### **Endpoint:** GET /get_attributes_with_name
Fetch attributes for your chosen model, which include parameters like "keywords" and specific "parameters".

**Python Code:**
```url = "https://opus5.p.rapidapi.com/get_attributes_with_name"
querystring = {"name": "House"}  # Replace with your desired model name

response = requests.get(url, headers=headers, params=querystring)
model_attributes = response.json()
print(model_attributes)
```

### **3. Customize and Create 3D Models**

After deciding on the attributes, you can customize and create your 3D model.

#### **a. Create Structure**
##### **Endpoint**: `POST /create_opus_structure`

**Python Code**:
```python
url = "https://opus5.p.rapidapi.com/create_opus_structure"
payload = {
    "name": "House",  
    "keywords": {
        "*": ["one_story"],
        "Window": ["modern"]
    },
    "texture_resolution": "2048"
}

response = requests.post(url, json=payload, headers=headers)
created_structure = response.json()
print(created_structure)
```
#### **b. Create Component**

##### **Endpoint**: `POST /create_opus_component`

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

### **4. Checking the Job Result**

Once the model is created, you can poll for the job result using the returned UUID from the creation step.

#### **Endpoint**: `GET /get_opus_job_result`

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

### **5. How to Change Model Extension**

To customize your 3D model's file extension, you'll utilize the `extensions` property in the payload. The provided schema highlights several potential values:

- `usd`: Pixar's Universal Scene Description format.
- `glb`: Binary version of the GL Transmission Format (GLTF).
- `gltf`: JSON-based 3D model format.
- `fbx`: Autodesk's Filmbox format.

For instance, if you wish to designate the model's extension to `glb`, you would adjust the `extensions` attribute in your request payload as follows:
```python
"extensions": ["glb"]
```

