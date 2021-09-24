Role Name
=========

A utility role to mirror various adhoc content (images, binaries...) for disconnected environments.

Requirements
------------


Role Variables
--------------

- ansible_name_module: The name of the module this role is part of. This is used to track context when this role is run in a playbook as part of other plays.  
- adhoc_images_bundle_file_name: Name of the xz format compressed artifact bundle file (e.g. operators-bundle.tar.xz)  
- adhoc_images_bundle_file_location: Location of the bundle file (e.g. operators-bundle.tar.xz)  
- adhoc_images_dir_bundle_staging: Location of the registry container file system on the controler that will be bound into the container registry to save all mirrored images.  
- adhoc_images_local_repository: The destination repository to story the images on the destination registry (e.g. openshift4)  
- adhoc_repository_host_fqdn: The host name of the repository used for binary content.
- dir_bundle_location: Location of the bundle on the host the role/playbook is run against.  
- default_operator_registry_username: Username to use to authenticate to the Source Operator registry.  
- default_operator_registry_password: Password to use to authenticate to the Source Operator registry.  
- default_operator_registry: Source Registry from which operators are mirrored (e.g. registry.redhat.io)  
- registry_container_name: The name of the container registry to use to mirror operators related contents (e.g. mirror-registry).  
- registry_container_dir: The name of the directory structure on the controller host that will be mounted into the registry container to save the container image layers and blobs. 
- registry_container_image: The name of the registry container to run (e.g. docker.io/library/registry:2).  
- adhoc_images_to_mirror: The various images that will be mirrored organized by source registry (e.g. redhat-registry, quay-registry...). This is a dictionary where each ky represents a source registry and contains properties like registry, username, password, mirrored_image_list, and mirror where :  
  - registry is the source registry for the group of images listed under the mirrored_image_list
  - username is the username to use to authenticate to the Source registry.
  - password is the password to use to authenticate to the Source registry. 
  - host_port is the name of the port on the controller to bind the container to (e.g. 50051). It has to be different for each operator index container.
  - mirrored_image_list is the list of images to be mirrored .

- local_repository: The destination repository to story the images on the destination registry (e.g. openshift4)  
- list_of_binaries_to_upload: List of binaries to push to the repository.
- binary_repository: The respository (directory within the content host) where the binaries are to be stored.
- registry_ca_cert: The CA of the registry or repository if applicable
- registry_host_fqdn: The IP or FQDN of the destination registry.
- registry_container_dir: The location of the container files on the controller where the registry container will save the image layers to be compressed and transported to the disconnected environment.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
To mirror and create the adhoc image bundle use the mirror-adhoc-images.yml:
```
   ansible-playbook mirror-adhoc-images.yml --ask-vault-pass -v
```
             
To push the adhoc image bundle content into the destination registry use the push-adhoc-images-to-registry.yml:
```
   ansible-playbook push-adhoc-images-to-registry.yml --ask-vault-pass -v
```
             
To push the adhoc binary content into the destination repository use the push-adhoc-binaries-to-content-host.yml:
```
   ansible-playbook push-adhoc-binaries-to-content-host.yml --ask-vault-pass -v
```

Installation
----------------
Before running the playbook, ensure you clone and run `ansible-galaxy role install -r requirements.yml -f -p roles` to download and install all dependencies. 


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
