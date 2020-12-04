# Create a fog05 descriptor that embeds the K8s descriptor

We can add a new k8s entity to the catalog passing a `basic_k8s.json` descriptor, inside an embedded fog05 descriptor `ek8s.json`

## The basic_k8s.json descriptor

The content of the `basic_k8s.json` file is:
```json
{
	"apiVersion":"apps/v1",
	"kind":"Deployment",
	"metadata":{
		"name":"nginx-deployment",
		"labels":{"app":"nginx"}
	},
	"spec":{
		"replicas":3,
		"selector":{
			"matchLabels":{"app":"nginx"}
		},
		"template":{
			"metadata":{
				"labels":{"app":"nginx"}
			},
			"spec":{
				"containers":[{
					"name":"nginx",
					"image":"nginx:1.14.2",
					"ports":[{
						"containerPort":80
					}]
    			}]
		    }
		}
	}
}
```

## The embedded `ek8s.json` descriptor

The content of the `ek8s.json` file is:

```json
{
    "id": "example-entity-k8s",
    "name": "example k8s entity",
    "version": "0.2.1",
    "entity_version": "0.0.1",
    "description": "this is an example entity",
    "fdus": [
        {
            "id": "nginx-k8s-fdu",
            "name": "nginx component",
            "version": "0.2.1",
            "fdu_version": "0.0.1",
            "description": "alpine nginx k8s",
            "hypervisor": "cloud",
            "computation_requirements": { "cpu_arch": "x86_64", "cpu_min_freq": 0, "cpu_min_count": 1, "ram_size_mb": 128, "storage_size_mb": 64 },
            "hypervisor_specific": "eyJhcGlWZXJzaW9uIjoiYXBwcy92MSIsImtpbmQiOiJEZXBsb3ltZW50IiwibWV0YWRhdGEiOnsibmFtZSI6Im5naW54LWRlcGxveW1lbnQiLCJsYWJlbHMiOnsiYXBwIjoibmdpbngifX0sInNwZWMiOnsicmVwbGljYXMiOjMsInNlbGVjdG9yIjp7Im1hdGNoTGFiZWxzIjp7ImFwcCI6Im5naW54In19LCJ0ZW1wbGF0ZSI6eyJtZXRhZGF0YSI6eyJsYWJlbHMiOnsiYXBwIjoibmdpbngifX0sInNwZWMiOnsiY29udGFpbmVycyI6W3sibmFtZSI6Im5naW54IiwiaW1hZ2UiOiJuZ2lueDoxLjE0LjIiLCJwb3J0cyI6W3siY29udGFpbmVyUG9ydCI6ODB9XX1dfX19fQo=",
            "interfaces": [],
            "connection_points": [],
            "migration_kind": "COLD",
            "depends_on": [],
            "storage": [],
            "replicas":2
        }
    ],
    "virtual_links": []
}
```

