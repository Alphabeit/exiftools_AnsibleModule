# exiftool X ansible

Ansible Role to overwrite the metadata of photos with ```exiftool```. 



## Backstory

I own a lots of photos. So why I installed at home a photo archive application. 
But I didn't take care about the metadata - until today. That why I need to change lots of metadata at once.

One solution does call ```exiftool```. With these is possible to change the metadata of multiple photos.
And because I use Ansible at work, I decided to create a script in this language.



## How to work

The role does change the metadata of all photos inside one folder at the same time. The folder is specified during execution.


```text
[exiftool : ask, from which folder the phots should edit]
Please enter path of folder with photos, who should edit:
 /path/to/folder/with/photos
```

> Please enter the full path, beginning by ```/```.


---

The file ```/exiftool/templates/_meta.yaml``` has two roles, depending on his location. 

```text
exiftool
├── tasks
└── templates
    └── _meta.yaml
```

```yaml
Title: # Example of a Title, leave empty in template
```

Inside the role itself, does the file work as template. As template, you can define the **flags**, which the role should ensure to set. 

> Please leave the values from the template empty.

By executing, the role ask the user to define the values. It's also allowed to leave the **flags** empty. Empty **flags** won't get writen on photos.

```text
[exiftool : ask for undefined vars]
Var "Caption" is not set. Do you want to set a value? When not, leave empty:
 on a sunny Day
```

> You can add or remove as much **flags** you like. But the role dindn't prove the **flags** about correctness - please consider it. 

---

```text
folder_with_photos
├── photo_one.JPG
├── photo_two.JPG
├── photo_three.JPG
└── _meta.yaml
```

```yaml
Title: Example of a Title, fell free to use in metafile
```

The second option is, to copy the file inside the folder, where the photos been who about to get changed.

The role will read the ```_meta.yaml``` first. Every **flag**, who get defined with this new metafile, won't need to get asked anymore. The flag is predefined.

> As example, when ```Title``` is already defined with the new file - the role wouldn't ask anymore about the ```Title```.

> I added some examples as comments how values could look like. Please look inside the template.

You can also add **flags** inside the new metafile, who won't be in the template.



## How to use

Add it to your Ansible Infrastructure as role and execute over following block inside a playbook. 

```yaml
- name: chance metadata of photos
  ansible.builtin.include_role:
    name: exiftool
```


## Dev Enviroment

Greated on a Arch enviroment.


## License 

Feel free to use.

