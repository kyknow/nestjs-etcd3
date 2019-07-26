
# Nestjs Etcd3

Etcd3 for NestJs.


### Installation

**Yarn**
```bash
yarn add nestjs-etcd3
```

**NPM**
```bash
npm install nestjs-etcd3 --save
```

### Getting Started
Let's register the EtcdModule in `app.module.ts`

```typescript
import { Module } from '@nestjs/common'
import { EtcdModule} from 'nestjs-etcd3'

@Module({
    imports: [
        EtcdModule.root({
            hosts: 'http://127.0.0.1:2379',
        }),
    ],
})
export class AppModule {}
```
Options
```typescript
interface EtcdModuleOptions {
    /**
     * Optional client cert credentials for talking to etcd. Describe more
     * {@link https://coreos.com/etcd/docs/latest/op-guide/security.html here},
     * passed into the createSsl function in GRPC
     * {@link https://grpc.io/grpc/node/grpc.credentials.html#.createSsl__anchor here}.
     */
    credentials?: {
        rootCertificate: Buffer;
        privateKey?: Buffer;
        certChain?: Buffer;
    };
    /**
     * Internal options to configure the GRPC client. These are channel options
     * as enumerated in their [C++ documentation](https://grpc.io/grpc/cpp/group__grpc__arg__keys.html).
     * For example:
     *
     * ```js
     * const etcd = new Etcd3({
     *   // ...
     *   grpcOptions: {
     *     'grpc.http2.max_ping_strikes': 3,
     *   },
     * })
     * ```
     */
    grpcOptions?: ChannelOptions;
    /**
     * Etcd password auth, if using.
     */
    auth?: {
        username: string;
        password: string;
    };
    /**
     * A list of hosts to connect to. Hosts should include the `https?://` prefix.
     */
    hosts: string[] | string;
    /**
     * Duration in milliseconds to wait while connecting before timing out.
     * Defaults to 30 seconds.
     */
    dialTimeout?: number;
    /**
     * Backoff strategy to use for connecting to hosts. Defaults to an
     * exponential strategy, starting at a 500 millisecond
     * retry with a 30 second max.
     */
    backoffStrategy?: IBackoffStrategy;
    /**
     * Whether, if a query fails as a result of a primitive GRPC error, to retry
     * it on a different server (provided one is available). This can make
     * service disruptions less-severe but can cause a domino effect if a
     * particular operation causes a failure that grpc reports as some sort of
     * internal or network error.
     *
     * Defaults to false.
     */
    retry?: boolean;
}
```
That's it!