# Node VPS Deployment

A simple GitHub action that allows everyone to deploy to a remote server that's using PM2 _easily_

## How to use the action?
```yml
steps:
  - uses: actions/checkout@v2
  
  - name: Deploy to Staging
    uses: Techie-Pi/node-vps-deployment@main
    with:
      remote-path: "~/deployment/staging"
      host: 123.123.123.123
      username: "ubuntu"
      port: 2080
      password: ${{ secrets.staging-password }}
      pm2-id: "staging"
```

## How does it work?
The action does the following:
1. Copies the repository contents to the remote server on the specified folder
2. Runs ``npm ci``
3. Runs ``pm2 restart <id>`` with the provided ID/Name

## Input arguments
### Required
- ``remote-path`` - _``Where do you want to copy the files to?``_
- ``host`` - _``What's the host IP address?``_
- ``username`` - _``What's the username that you're going to login into``_
- ``port`` - _``What's the port of SSH?``_ (default: ``22``)
- ``password`` - _``What's the password of the user?``_ (Note: in the future SSH Keys will be supported)
- ``pm2-id`` - _``What's the ID/Name of the PM2 application?``_

> Note: Although sensitive information such as ``password`` is used through the input arguments, it's recommended to save it on ``Secrets``
