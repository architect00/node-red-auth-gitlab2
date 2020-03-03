# Node-RED Authentication with Gitlab

[Node-RED](https://nodered.org) plugin for authenticating users with Gitlab.

This modules lets you restrict access to the Node-RED editor to specific gitlab
users. Code-base and README from [node-red-auth-github](https://github.com/node-red/node-red-auth-github).

**Note:** this requires Node-RED 0.17 or later


## Install

In your Node-RED user directory, typically `~/.node-red`:

    $ npm install strassi/node-red-auth-gitlab2

## Usage

### Register a new gitlab application

To enable access control with gitlab, you must first [register a new application
on your gitlab account](https://docs.gitlab.com/ee/integration/oauth_provider.html#adding-an-application-through-the-profile).

Once created, you will be provided a _Client ID_ and _Client Secret_ that
you will need to use to configure the authentication plugin.

### Configure `adminAuth`

Access control for the Node-RED editor is configured in your `settings.js` file
using the `adminAuth` property.

    adminAuth: require('node-red-auth-gitlab2')({
        clientID: GITLAB_CLIENT_ID,
        clientSecret: GITLAB_CLIENT_SECRET,
        baseURL: "http://localhost:1880/",
	gitlabURL: "https://your.gitlab.local/",
        users: [
           { username: "pepe",permissions: ["*"]}
        ]
    })

The `baseURL` property is the URL used to access the Node-RED editor.

The `users` property is the list of gitlab users who are allowed to access the
editor. It is the same as used by `adminAuth` as described in the [security documentation](http://nodered.org/docs/security), but without the `password` property.

A default user can be specified by adding a `default` property to the options object:

        users: [
           ...
        ],
        default: {
            permissions: "read"
        }

## Copyright and license

Copyright JS Foundation and other contributors, http://js.foundation under [the Apache 2.0 license](LICENSE).
