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
2. Runs ``npm ci``or ``yarn install``
3. Runs ``pm2 restart <id>`` with the provided ID/Name

## Input arguments
### Required
- ``remote-path`` - Where do you want to copy the files to?
- ``host`` - _What's the host IP address?
- ``username`` - What's the username that you're going to login into
- ``port`` - What's the port of SSH? (default: ``22``)
- ``password`` - What's the password of the user?`` (Note: in the future SSH Keys will be supported)
- ``automatic-pre-deploy`` - Should deploy automatically (default ``true``)
- ``yarn`` - Use yarn instead of npm (default ``false``)
- ``pm2-id`` - What's the ID/Name of the PM2 application?

> Note: Although sensitive information such as ``password`` is used through the input arguments, it's recommended to save it on ``Secrets``
