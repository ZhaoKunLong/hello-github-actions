## Welcome to "Hello World" with GitHub Actions

This course will walk you through writing your first action and using it with a workflow file. 

**Ready to get started? Navigate to the first issue.**


Step 
1. Create DockerFile
  -  create DockerFile, DockerFile add the entrypoint.sh into docker. End run the entrypoint
  - ENTRYPOINT in docker is run a cmd
2. Create entrypoint.sh
  - only for the docker. When docker run will execute `ENTRYPOINT` cmd.
3. Create action.yml
  - we'll define the action.yml file which contains the metadata for our action.
  - This is for the github workflow metadata. will define all the input and image use.
4. Create the workflow 
  - Execute base on the github event.