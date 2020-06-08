# dcos-besu

## DC/OS Setup

```
dcos package repo add besu-repo --index=0 https://github.com/iss-lab/dcos-besu/releases/download/v1.4.5/besu-repo.json
```

## Installing

Bes64 encode an array of private keys for your nodes, the first one belongs to the bootnode:

```
echo '["0fd4aecd8f02b24f468325aa06e1428ab8076d283bac3ed804c9f70187dedb63","47c63c0afd1a85b16915934a2d75cf5a0d3bd13c509d6ee9d7ef1315a36bdc0a","35dcc853354b24e98889fa4b2e214d5e92e759ef8312bb6a444bad3182187b68","d38e71552943e18061fdb44a72eca14ea193e0505a7ead404864f9840e275b49","7fd74d74209b7dd06a556b5745f9f4aa85b0ac54ee72bd0969929096210a666a"]' | base64 -w 0
```

Private Keys Base64:

```
WyIwZmQ0YWVjZDhmMDJiMjRmNDY4MzI1YWEwNmUxNDI4YWI4MDc2ZDI4M2JhYzNlZDgwNGM5ZjcwMTg3ZGVkYjYzIiwiNDdjNjNjMGFmZDFhODViMTY5MTU5MzRhMmQ3NWNmNWEwZDNiZDEzYzUwOWQ2ZWU5ZDdlZjEzMTVhMzZiZGMwYSIsIjM1ZGNjODUzMzU0YjI0ZTk4ODg5ZmE0YjJlMjE0ZDVlOTJlNzU5ZWY4MzEyYmI2YTQ0NGJhZDMxODIxODdiNjgiLCJkMzhlNzE1NTI5NDNlMTgwNjFmZGI0NGE3MmVjYTE0ZWExOTNlMDUwNWE3ZWFkNDA0ODY0Zjk4NDBlMjc1YjQ5IiwiN2ZkNzRkNzQyMDliN2RkMDZhNTU2YjU3NDVmOWY0YWE4NWIwYWM1NGVlNzJiZDA5Njk5MjkwOTYyMTBhNjY2YSJdCg==
```

Do the same for the matching public keys:

```
echo '["c1979a8a48693db804316b5acebe35e11731e1fb1c9c21ff7268ab25db6f6e03390a429b83cf0ec0865a7205f2669ec1ace652a3def11e2e01571c74939cbe22","e40129f02c9e29a02049668346d4777bb55809042746882b33b20a8b5a7310eb5f107a53f0aa3da766ee77f401557a79c0c328329ea48bf0996c6c9dff817f76","a3e4af081a0ab853c959b9acd0596f818b91a9409b9d04c50af055072c929abfa340e14111dcfa76e049fdb16bb9198e722d5e7be3e8ef37562ea0d0ce1eda11","8f4e444a73034236ab4244c7a572aa2c6198b9e0d483ef17bf4b751cac5c0370bc527a5b0c5d01aa3ef41704af838c74730aeecac0f0c22dc4c17b0a9f03ad76","51729f1b4186db1701e13d9e71b7b4f0a35e0cc1f480c904c5e758b5b76936685dccde490c623a79f6c6c5d1dfd3eae37d35101e1a9a2d06536074562dd77604"]' | base64 -w 0
```

Public Keys Base64:

```
WyJjMTk3OWE4YTQ4NjkzZGI4MDQzMTZiNWFjZWJlMzVlMTE3MzFlMWZiMWM5YzIxZmY3MjY4YWIyNWRiNmY2ZTAzMzkwYTQyOWI4M2NmMGVjMDg2NWE3MjA1ZjI2NjllYzFhY2U2NTJhM2RlZjExZTJlMDE1NzFjNzQ5MzljYmUyMiIsImU0MDEyOWYwMmM5ZTI5YTAyMDQ5NjY4MzQ2ZDQ3NzdiYjU1ODA5MDQyNzQ2ODgyYjMzYjIwYThiNWE3MzEwZWI1ZjEwN2E1M2YwYWEzZGE3NjZlZTc3ZjQwMTU1N2E3OWMwYzMyODMyOWVhNDhiZjA5OTZjNmM5ZGZmODE3Zjc2IiwiYTNlNGFmMDgxYTBhYjg1M2M5NTliOWFjZDA1OTZmODE4YjkxYTk0MDliOWQwNGM1MGFmMDU1MDcyYzkyOWFiZmEzNDBlMTQxMTFkY2ZhNzZlMDQ5ZmRiMTZiYjkxOThlNzIyZDVlN2JlM2U4ZWYzNzU2MmVhMGQwY2UxZWRhMTEiLCI4ZjRlNDQ0YTczMDM0MjM2YWI0MjQ0YzdhNTcyYWEyYzYxOThiOWUwZDQ4M2VmMTdiZjRiNzUxY2FjNWMwMzcwYmM1MjdhNWIwYzVkMDFhYTNlZjQxNzA0YWY4MzhjNzQ3MzBhZWVjYWMwZjBjMjJkYzRjMTdiMGE5ZjAzYWQ3NiIsIjUxNzI5ZjFiNDE4NmRiMTcwMWUxM2Q5ZTcxYjdiNGYwYTM1ZTBjYzFmNDgwYzkwNGM1ZTc1OGI1Yjc2OTM2Njg1ZGNjZGU0OTBjNjIzYTc5ZjZjNmM1ZDFkZmQzZWFlMzdkMzUxMDFlMWE5YTJkMDY1MzYwNzQ1NjJkZDc3NjA0Il0K
```

Create an `options.json` file with these values:

```
{
  "service": {
    "name": "besu"
  },
  "node": {
    "count": 5,
    "cpus": 1,
    "mem": 1024,
    "disk": 1024
  },
  "besu": {
    "BESU_PRIVATE_KEY_ARRAY_BASE64": "WyIwZmQ0YWVjZDhmMDJiMjRmNDY4MzI1YWEwNmUxNDI4YWI4MDc2ZDI4M2JhYzNlZDgwNGM5ZjcwMTg3ZGVkYjYzIiwiNDdjNjNjMGFmZDFhODViMTY5MTU5MzRhMmQ3NWNmNWEwZDNiZDEzYzUwOWQ2ZWU5ZDdlZjEzMTVhMzZiZGMwYSIsIjM1ZGNjODUzMzU0YjI0ZTk4ODg5ZmE0YjJlMjE0ZDVlOTJlNzU5ZWY4MzEyYmI2YTQ0NGJhZDMxODIxODdiNjgiLCJkMzhlNzE1NTI5NDNlMTgwNjFmZGI0NGE3MmVjYTE0ZWExOTNlMDUwNWE3ZWFkNDA0ODY0Zjk4NDBlMjc1YjQ5IiwiN2ZkNzRkNzQyMDliN2RkMDZhNTU2YjU3NDVmOWY0YWE4NWIwYWM1NGVlNzJiZDA5Njk5MjkwOTYyMTBhNjY2YSJdCg==",
    "BESU_PUBLIC_KEY_ARRAY_BASE64": "WyJjMTk3OWE4YTQ4NjkzZGI4MDQzMTZiNWFjZWJlMzVlMTE3MzFlMWZiMWM5YzIxZmY3MjY4YWIyNWRiNmY2ZTAzMzkwYTQyOWI4M2NmMGVjMDg2NWE3MjA1ZjI2NjllYzFhY2U2NTJhM2RlZjExZTJlMDE1NzFjNzQ5MzljYmUyMiIsImU0MDEyOWYwMmM5ZTI5YTAyMDQ5NjY4MzQ2ZDQ3NzdiYjU1ODA5MDQyNzQ2ODgyYjMzYjIwYThiNWE3MzEwZWI1ZjEwN2E1M2YwYWEzZGE3NjZlZTc3ZjQwMTU1N2E3OWMwYzMyODMyOWVhNDhiZjA5OTZjNmM5ZGZmODE3Zjc2IiwiYTNlNGFmMDgxYTBhYjg1M2M5NTliOWFjZDA1OTZmODE4YjkxYTk0MDliOWQwNGM1MGFmMDU1MDcyYzkyOWFiZmEzNDBlMTQxMTFkY2ZhNzZlMDQ5ZmRiMTZiYjkxOThlNzIyZDVlN2JlM2U4ZWYzNzU2MmVhMGQwY2UxZWRhMTEiLCI4ZjRlNDQ0YTczMDM0MjM2YWI0MjQ0YzdhNTcyYWEyYzYxOThiOWUwZDQ4M2VmMTdiZjRiNzUxY2FjNWMwMzcwYmM1MjdhNWIwYzVkMDFhYTNlZjQxNzA0YWY4MzhjNzQ3MzBhZWVjYWMwZjBjMjJkYzRjMTdiMGE5ZjAzYWQ3NiIsIjUxNzI5ZjFiNDE4NmRiMTcwMWUxM2Q5ZTcxYjdiNGYwYTM1ZTBjYzFmNDgwYzkwNGM1ZTc1OGI1Yjc2OTM2Njg1ZGNjZGU0OTBjNjIzYTc5ZjZjNmM1ZDFkZmQzZWFlMzdkMzUxMDFlMWE5YTJkMDY1MzYwNzQ1NjJkZDc3NjA0Il0K",
    "BESU_BOOTNODE_PUBLIC_KEY_BASE64": "MHhjMTk3OWE4YTQ4NjkzZGI4MDQzMTZiNWFjZWJlMzVlMTE3MzFlMWZiMWM5YzIxZmY3MjY4YWIyNWRiNmY2ZTAzMzkwYTQyOWI4M2NmMGVjMDg2NWE3MjA1ZjI2NjllYzFhY2U2NTJhM2RlZjExZTJlMDE1NzFjNzQ5MzljYmUyMgo="
  }
}
```

Install the package

```
dcos package install besu --options=options.json
```

## Development

### Creating a github release

Update the release version in package.json, and then:

```
dcosdev release --keep 0 none
```

That command will fail, but it creates the correct `dist/besu-repo.json` which can be uploaded elsewhere, like Github.

```
GH_REPO="https://api.github.com/repos/iss-lab/dcos-besu"
GH_TAGS="$GH_REPO/releases/tags/v1.4.5"
AUTH="Authorization: token $github_api_token"
response=$(curl -sH "$AUTH" $GH_TAGS)
id=$(echo $response | jq .id)
GH_ASSET="https://uploads.github.com/repos/iss-lab/dcos-besu/releases/$id/assets"

curl --data-binary @"./dist/besu-repo.json" -H "Authorization: token $github_api_token" -H "Content-Type: application/vnd.dcos.universe.repo+json;charset=utf-8;version=v4" "$GH_ASSET?name=besu-repo.json"

curl --data-binary @"svc.yml" -H "Authorization: token $github_api_token" -H "Content-Type: text/yaml" "$GH_ASSET?name=svc.yml"
curl --data-binary @"./files/config.toml" -H "Authorization: token $github_api_token" -H "Content-Type: text/toml" "$GH_ASSET?name=config.toml"
curl --data-binary @"./files/genesis.json" -H "Authorization: token $github_api_token" -H "Content-Type: application/json" "$GH_ASSET?name=genesis.json"
```