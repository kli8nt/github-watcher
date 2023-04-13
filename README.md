# github-deployment-env

In GitHub, a deployment environment is a specific target environment, such as staging or production, where a particular version of your application is deployed for testing or use. When you deploy your code to a deployment environment in GitHub, you are essentially making it available to users or other parts of your application.

GitHub's deployment environment is triggered when someone makes changes to the repository, depending on how you have configured your deployment process. For example, you can set up automatic deployment to your staging environment every time a pull request is merged into the main branch. Alternatively, you can trigger deployments manually through the GitHub interface or via an API.

- [ ] Creating deployment

```python
# Set up the deployment parameters
data = {
    'ref': 'main',
    'environment': 'production',
    'required_contexts': [],
    'auto_merge': False,
    'payload': {},
    'task': 'deploy',
}

# Make the API request to create a deployment
response = requests.post(
    'https://api.github.com/repos/OWNER/REPO/deployments',
    headers=headers,
    json=data
)
```

- [ ] Make a deployment status and deployment url


```python
# Set up the deployment status parameters
data = {
    'state': 'success',
    'target_url': 'YOUR_DEPLOYMENT_ENVIRONMENT_URL',
    'description': 'Deployment succeeded!',
    'environment': 'production',
    'auto_inactive': True
}

# Make the API request to create a deployment status
response = requests.post(
    f'https://api.github.com/repos/OWNER/REPO/deployments/{deployment_id}/statuses',
    headers=headers,
    json=data
)
```

- [ ] Add a github deployment hook to trigger on pushs

```python
# Set up the webhook parameters
data = {
    'name': 'web',
    'active': True,
    'events': ['push'],
    'config': {
        'url': 'YOUR_DEPLOYMENT_URL',
        'content_type': 'json'
    }
}

# Make the API request to create a webhook
response = requests.post(
    f'https://api.github.com/repos/OWNER/REPO/hooks',
    headers=headers,
    json=data
)
```

--- that seems like all what we need for this part, of course all these repos and pieces of code will be in go and in one unified backend...



resources

https://github.com/previousnext/go-deploy-status


https://www.tech-otaku.com/web-development/using-cloudflare-api-manage-dns-records/


https://github.com/Konboi/ghooks
