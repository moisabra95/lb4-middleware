# lb4-middleware

[![GitHub stars](https://img.shields.io/github/stars/codejamninja/lb4-middleware.svg?style=social&label=Stars)](https://github.com/codejamninja/lb4-middleware)

> run express middleware in loopback 4

Please ★ this repo if you found it useful ★ ★ ★

## Features

- supports loopback 4
- supports express middleware
- supports typescript

## Installation

```sh
npm install --save lb4-middleware
```
Edit `src/sequence.ts`
```typescript
import {MiddlewareAction } from 'lb4-middleware';
...
export class MySequence implements SequenceHandler {
  constructor(
    ...
    //---------
    public middlewareAction: MiddlewareAction
    //---------
  ) {}

  async handle(context: RequestContext) {
    try {
      ...

      //---------
      await this.middlewareAction(context);
      //---------

      const result = await this.invoke(route, args);
      this.send(response, result);
    } catch (err) {
      this.reject(context, err);
    }
  }
```
Edit `src/application.ts`

```typescript
import {MiddlewareComponent} from 'lb4-middleware';

 ...
 constructor(options: ApplicationConfig = {}) {
  ...
  //---------
  this.component(MiddlewareComponent);
  //---------
  ...
 }
```

In Controller
```typescript
import { middleware, NextFunction } from 'lb4-middleware';
import {  Request,  get,Response} from '@loopback/rest';

@middleware((_req: Request, _res: Response, next: NextFunction) => {
  console.log('middleware');
  return next();
})

@get('/ping')

ping(): object {
  return {
    greeting: 'Hello from LoopBack',
    date: new Date(),
    url: this.req.url,
    headers: Object.assign({}, this.req.headers)
  };
}

```

## Dependencies

- [NodeJS](https://nodejs.org)

## Usage

[Contribute](https://github.com/codejamninja/lb4-middleware/blob/master/CONTRIBUTING.md) usage docs

## Support

Submit an [issue](https://github.com/codejamninja/lb4-middleware/issues/new)

## Screenshots

[Contribute](https://github.com/codejamninja/lb4-middleware/blob/master/CONTRIBUTING.md) a screenshot

## Contributing

Review the [guidelines for contributing](https://github.com/codejamninja/lb4-middleware/blob/master/CONTRIBUTING.md)

## License

[MIT License](https://github.com/codejamninja/lb4-middleware/blob/master/LICENSE)

[Jam Risser](https://codejam.ninja) © 2019

## Changelog

Review the [changelog](https://github.com/codejamninja/lb4-middleware/blob/master/CHANGELOG.md)

## Credits

- [Jam Risser](https://codejam.ninja) - Author

## Support on Liberapay

A ridiculous amount of coffee ☕ ☕ ☕ was consumed in the process of building this project.

[Add some fuel](https://liberapay.com/codejamninja/donate) if you'd like to keep me going!

[![Liberapay receiving](https://img.shields.io/liberapay/receives/codejamninja.svg?style=flat-square)](https://liberapay.com/codejamninja/donate)
[![Liberapay patrons](https://img.shields.io/liberapay/patrons/codejamninja.svg?style=flat-square)](https://liberapay.com/codejamninja/donate)
