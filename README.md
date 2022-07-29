# confignator

Type-safe declaration configuration loading, parsing, and validation from:
- configuration files
- environment variables
- and CLI flags

[ **Work in Progress** ]

### Example

```ts
import type { ConfigSchema } from 'confignator'
import { V, config_resolver } from 'confignator'

type Config = {
  backend_nodes: string[]
}

const config_schema: ConfigSchema<Config> = {
  backend_nodes: {
    validator: V.list(V.str),
    env: 'BACKEND_NODES',
    default: ['127.0.0.1'],
  },
}

const resolve_config = config_resolver<Config>(config_schema)

const get_env = (name: string) => process.env[name]

export const config = resolve_config({ get_env })
```
