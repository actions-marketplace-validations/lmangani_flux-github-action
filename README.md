# <img src="https://user-images.githubusercontent.com/1423657/162720189-976cc0cc-7511-4278-a942-9c4e7cc9148a.png" width=250 />

# Flux GitHub Action

This action sets up a [Fluxpipe](https://github.com/metrico/fluXpipe) runner to execute [Flux](https://github.com/influxdata/flux) scripts.

# Usage

```yaml
steps:
  - name: Flux in GitHub Actions
    uses: lmangani/flux-github-action@main
```

## Example
### CSV Output
```yaml
jobs:
  fluxpipe:
    runs-on: ubuntu-latest
    name: Run a Flux Script
    steps:
      - name: Flux Run
        id: flux
        uses: lmangani/flux-github-action@csv
        with:
          flux-script: 'import "array" import "runtime" array.from(rows: [{version: runtime.version()}])'
      - name: Flux Result
        run: echo "${{ steps.flux.outputs.result }}"
```
```csv
#datatype,string,long,string
#group,false,false,false
#default,_result,,
,result,table,version
,,0,v0.192.0
```

### JSON Output
```yaml
jobs:
  fluxpipe:
    runs-on: ubuntu-latest
    name: Run a Flux Script
    steps:
      - name: Flux Run
        id: flux
        uses: lmangani/flux-github-action@json
        with:
          flux-script: 'import "array" import "runtime" array.from(rows: [{version: runtime.version()}])'
      - name: Flux Result
        run: echo "${{ steps.flux.outputs.result }}"
```
```javascript
[
	{
		columns: {
			result: {
				index: 1,
				type: string
			},
			table: {
				index: 2,
				type: long
			},
			version: {
				index: 3,
				type: string
			}
		},
		rows: [
			{
				result: _result,
				table: 0,
				version: v0.192.0
			}
		]
	}
]
```


# License
This project released under the [MIT License](LICENSE)
