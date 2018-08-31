# Huh?

This is a [GitHub webhook](https://developer.github.com/webhooks/) to trigger a function that is responsible for building a Hugo blog. If you set this up on your GitHub repository, this function will get called on certain repository events which will trigger a rebuild of your Hugo blog.

[This is based on this example from the Serverless framework.](https://github.com/serverless/examples/blob/master/aws-node-github-webhook-listener/handler.js)

So you set up this Lambda function behind an API Gateway endpoint and you give the HTTP endpoint to your GitHub Webhook. This function will then asynchronously call your other Lambda function ([example here](https://github.com/wnka/hugo-lambda)) that is then responsible for building your Hugo website. Why do we need to chain functions like this? Well, building a Hugo site could take some time and API Gateway functions are limited to 30 seconds. So we just use this function to kickoff the real work.

# Environment Variables

Here are the environment variables you MUST set on this Lambda function.

| Name                  | Description                                                       | Example       |
|-----------------------|-------------------------------------------------------------------|---------------|
| GITHUB_WEBHOOK_SECRET | The secret you configured on your GitHub webhook                  | asdfjkl       |
| BUILD_FUNCTION        | The main function that is responsible for building your Hugo blog | build-my-blog |
