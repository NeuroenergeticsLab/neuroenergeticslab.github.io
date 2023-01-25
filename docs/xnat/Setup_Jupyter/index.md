---
layout: default
title: Pyxnat
parent: Data Pipeline
has_children: false
nav_order: 4
---

# Setup

Here you can find help with the setup of Jupyter Notebook and access data on server using Pyxnat.

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
 

***


## Access the data on XNAT with pyxnat

Pyxnat library provides a nice API interface to access data on XNAT.

The data is organized hierarchically:

`Project`
└── `Subject`
    └── `Experiment`
        └── `Scan`
            └── `Resource`
                └── `File`

### Setup the connection
- Create a configuration file

    On terminal connected to the remote server:

    ```bash
    cd
    echo '{"server": "http://10.0.3.12", "user": "<user>", "password": "<password>"}' >> xnat_config.cfg
    ```

- Connect to a project

    ```python
    import pyxnat
    interface = pyxnat.Interface(config='<path to config file>')
    project = interface.select.project('<project name>')
    ```

- Check the connection

    ```python
    print(project.exists())
    >>> True
    ```

### Projects

- List all available projects on XNAT
```python
for project in interface.select.projects():
    print(project.label())
```

- Select a project and check if it exists (`project` is singular here and plural in the previus example)
```python
project = interface.select.project('<project label>')
print(project.exists())
>>> True
```

### Subjects

- List all the subjects in a project

    ```python
    for subject in project.subjects():
        print(subject.label())
    ```

- Select one

    ```python
    subject = project.subject('<subject label>')
    print(subject.exists())
    >>> True
    ```

### Sessions

- Each subject can have multiple sessions (e.g. before-after). In pyxnat they are called `experiment`

    ```python
    for session in subject.experiments():
        print(session.label())

    session = subject.experiment('<session label>')
    print(session.exists())
    >>> True
    ```

### Scans

- List the scan ids (numbers) and descriptions
    ```python
    for scan in session.scans():
        print(scan.label(), scan.attrs.mget({'type'})[0])
    >>> 1 Localizer
    >>> 2 MPRAGE
    >>> ...
    ```

- Select a scan (should use scan label: number as a string)

    ```python
    scan = session.scan('<scan label>')
    print(scan.exists())
    >>> True
    ```

### Resources

- Resource can be a different file format (e.g. [DICOM](../../Glossary/glossary.md/#DICOM "Digital imaging and communications in medicine") or [NIFTI](../../Glossary/glossary.md/#NIFTI "Neuroimaging informatics technology initiative"))

    ```python
    for resource in scan.resources():
        print(resource.label())

    resource = scan.resource('<resource label>')
    print(resource.exists())
    >>> True
    ```

### Files

- A resource can have multiple files (e.g. separate file after each processing step)

    ```python
    for file in resource.files():
        print(file.label())
    ```

- Access the full path of a file stored on XNAT

    ```python
    file = resource.file('<file label>')
    print(file.exists())
    >>> True

    print(file._uri)
    >>> '/data/projects/<project label>/subjects/<subject label>/experiments/<session label>/scans/<scan label>/resources/<resource label>/files/<file label>'
    ```


### Download data

- Call `.get()` function on a `Resource` or `File` object. For example, to download all files in a resource:

    ```python
    resource = project.subject('<subject id>').experiment('<session id>').scan('<scan id>').resource('<resource id>')
    resource.get('<local directory path>') # this is where the files (in a zip archive) will be downloaded to
    ```

### Upload data

- Similarly, can call `.insert()` funciton on `Resource` or `File`. E.g. to upload a file to a resource:

    ```python
    file = resource.file('<remote filename>') # this is the name the file will appear on XNAT
    file.insert('<local file path>') # this is the path to the file stored locally
    ```

- Check that the file exists on XNAT:

    ```python
    print(file.exists(), file._uri)
    >>> True remote/file/path
    ```

### Delete data

- Delete a file or a resource

    ```python
    file.delete()
    print(file.exists())
    >>> False
    ```

### Simple processing example

- Go through each subject in a `test` project, download files from `nifti` resource for `mprage` scans, extract the brains using fsl `bet` command and upload the result back to the `nifti` resource

    ```python
    import pyxnat
    import os

    interface = pyxnat.Interface(config='/home/roman/xnat_config.cfg')
    project = interface.project('test')

    for subject in project.subjects():
        for session in subject.experiments():
            for scan in session.scans():

                if scan.attrs.mget({'type'})[0] == 'mprage':

                    resource = scan.resource('nifti')
                    file = resource.file('mprage.nii.gz')
                    assert file.exists(), 'Mprage file does not exist for subject {}'.format(subject.label())

                    # Download the file
                    t1_filename = file.get('/home/roman/Downloads')

                    # Extract the brain
                    t1_filename = t1_filename.replace('.nii.gz', '') # remove the extension
                    brain_filename = t1_filename + '_brain'
                    ! bet {t1_filename} {brain_filename}

                    # Uplaod the file
                    remote_name = os.path.basename(brain_filename) + '.nii.gz'
                    local_name = brain_filename + '.nii.gz'
                    resource.file(remote_name).insert(local_name)

                    # Check that the upload worked
                    assert resource.file(remote_name).exists(), 'Upload did not work for subject {}'.format(subject)
    ```
