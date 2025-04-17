# poetry and uv project dependency mangement template
This repo is to show how to manage project with peotry and uv togther. 

Even though uv can installation, resolution, and compilation with high speed, but it does not support `uv add` like Poetry's `poetry add`, especially not with group targeting like `--group dev.`

Therefore, it is better to specifically apply them to dependency management tasks that they are good at


## Dependence management related tasks and its corresponding tools

| Task       | Tool |
|:-----------|------------:|
| Add/edit dependencies      | ✅ Poetry | 
| Lock file generation        | ✅ Poetry  | 
| Fast installation    | ✅ uv  | 
| Install by group   | ✅ uv via --groups=... | 

## Dependence management procedures

1. set the `pyproject.toml` with `dynamic = ["dependencies"]` like this repo  

2. add dependencies to your main project with peotry and it will generate `poetry.lock` file
    
    eg. 
        
    `poetry add numpy` 
3. add dependencies to specific groups and add line to `poetry.lock` file for the groups
   
   eg.

    `poetry add pytest --group dev`
    `poetry add ruff --group unittest`

4. handle the installation for your main project with uv
    
    eg.
    
    `uv pip install -r <(uv pip compile poetry.lock)`

5. handle the installation for specific groups
    
    eg.
    
    `uv pip install -r <(uv pip compile --groups=dev poetry.lock)`
    
    `uv pip install -r <(uv pip compile --groups=unittest poetry.lock)`
    

