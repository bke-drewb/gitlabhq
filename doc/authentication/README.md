# External Authentication

GitLab leverages OmniAuth to allow users to sign in using Twitter, Google and other popular services. Configuring OmniAuth does not prevent standard GitLab authentication or LDAP (if configured) from continuing to work. Users can choose to sign in using any of the configured mechanisms.

+ [Initial OmniAuth Configuration](#initial-omniauth-configuration)
+ [Supported Providers](#supported-providers)

### Initial OmniAuth Configuration

Before configuring individual OmniAuth providers there are a few global settings that need to be verified.

1. Open the configuration file

```sh
cd /home/git/gitlab

sudo -u git -H editor config/gitlab.yml
```

2. Find the section dealing with OmniAuth. The section will look similar to the following.

```
  ## OmniAuth settings
  omniauth:
    # Allow login via Twitter, Google, etc. using OmniAuth providers
    enabled: false

    # CAUTION!
    # This allows users to login without having a user account first (default: false).
    # User accounts will be created automatically when authentication was successful.
    allow_single_sign_on: false
    # Locks down those users until they have been cleared by the admin (default: true).
    block_auto_created_users: true

    ## Auth providers
    # Uncomment the following lines and fill in the data of the auth provider you want to use
    # If your favorite auth provider is not listed you can use others:
    # see https://github.com/gitlabhq/gitlab-public-wiki/wiki/Working-custom-omniauth-provider-configurations
    # The 'app_id' and 'app_secret' parameters are always passed as the first two
    # arguments, followed by optional 'args' which can be either a hash or an array.
    providers:
      # - { name: 'google_oauth2', app_id: 'YOUR APP ID',
      #     app_secret: 'YOUR APP SECRET',
      #     args: { access_type: 'offline', approval_prompt: '' } }
      # - { name: 'twitter', app_id: 'YOUR APP ID',
      #     app_secret: 'YOUR APP SECRET'}
      # - { name: 'github', app_id: 'YOUR APP ID',
      #     app_secret: 'YOUR APP SECRET',
      #     args: { scope: 'user:email' } }
```

3. Change `enabled` to `true`.
4. Consider the next two configuration options: `allow_single_sign_on` and `block_auto_created_users`. 
    * `allow_single_sign_on` defaults to `false`. If `false` users must be created manually or they will not be able to sign in via OmniAuth.
    * `block_auto_created_users` defaults to `true`. If `true` auto created users will be blocked by default and will have to be unblocked by an administrator before they are able to sign in.
    * **Note:** If you set `allow_single_sign_on` to `true` and `block_auto_created_users` to `false` please be aware that any user on the Internet will be able to successfully sign in to your GitLab without administrative approval. 

### Supported Providers

+ [GitHub](github.md)

