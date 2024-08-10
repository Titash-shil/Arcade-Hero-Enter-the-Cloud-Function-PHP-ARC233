# Arcade Hero: Enter the Cloud Function PHP || [ARC233]([https://www.cloudskillsboost.google/focuses/98842?parent=catalog](https://www.cloudskillsboost.google/focuses/98839?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=34941169)) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell

```
export REGION=
```
```

gcloud config set compute/region $REGION
export PROJECT_ID=$(gcloud config get-value project)


mkdir quicklab && cd quicklab

cat > index.php <<'EOF_END'
<?php
use Google\CloudFunctions\FunctionsFramework;
use Psr\Http\Message\ServerRequestInterface;

// Register the function with Functions Framework.
// This enables omitting the `FUNCTIONS_SIGNATURE_TYPE=http` environment
// variable when deploying. The `FUNCTION_TARGET` environment variable should
// match the first parameter.
FunctionsFramework::http('helloHttp', 'helloHttp');

function helloHttp(ServerRequestInterface $request): string
{
  $name = 'World';
  $body = $request->getBody()->getContents();
  if (!empty($body)) {
    $json = json_decode($body, true);
    if (json_last_error() != JSON_ERROR_NONE) {
      throw new RuntimeException(sprintf(
        'Could not parse body: %s',
        json_last_error_msg()
      ));
    }
    $name = $json['name'] ?? $name;
  }
  $queryString = $request->getQueryParams();
  $name = $queryString['name'] ?? $name;

  return sprintf('Hello, %s!', htmlspecialchars($name));
}

EOF_END


cat > composer.json <<EOF_END
{
   "require": {
       "google/cloud-functions-framework": "^1.1"
   }
}

EOF_END

gcloud functions deploy cf-demo \
  --gen2 \
  --runtime php82 \
  --entry-point helloHttp \
  --source . \
  --region $REGION \
  --trigger-http \
  --allow-unauthenticated \
  --quiet
```

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
