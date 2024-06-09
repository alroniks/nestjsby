# Першыя крокі

У гэтым наборы артыкулаў вы даведаецеся **асноўныя асновы** Nest. Каб азнаёміцца ​​з асноўнымі будаўнічымі блокамі прыкладанняў Nest, мы створым базавую праграму CRUD з функцыямі, якія ахопліваюць шмат пытанняў на пачатковым узроўні.

## Мова

Мы любім [TypeScript](https://www.typescriptlang.org/) , але больш за ўсё мы любім [Node.js.](https://nodejs.org/en/) Вось чаму Nest сумяшчальны як з TypeScript, так і **з чыстым JavaScript** . Nest выкарыстоўвае найноўшыя моўныя магчымасці, таму, каб выкарыстоўваць яго з ванільным JavaScript, нам спатрэбіцца кампілятар [Babel](https://babeljs.io/) .

Мы ў асноўным будзем выкарыстоўваць TypeScript у прадстаўленых прыкладах, але вы заўсёды можаце **пераключыць фрагменты кода** на сінтаксіс JavaScript (проста націсніце, каб пераключыць кнопку мовы ў правым верхнім куце кожнага фрагмента).

## Перадумовы

Пераканайцеся, што ў вашай аперацыйнай сістэме ўсталяваны [Node.js](https://nodejs.org) (версія &gt;= 16).

## Усталяваць

З [Nest CLI](/cli/overview) наладзіць новы праект даволі проста. З усталяваным [npm](https://www.npmjs.com/) вы можаце стварыць новы праект Nest з дапамогай наступных каманд у тэрмінале АС:

```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

:::info **Падказка** Каб стварыць новы праект з [больш строгім](https://www.typescriptlang.org/tsconfig#strict) наборам функцый TypeScript, перадайце сцяжок `--strict` камандзе `nest new` . :::

Будзе створаны каталог `project-name` , будуць устаноўлены модулі вузлоў і некалькі іншых шаблонных файлаў, а таксама будзе створаны каталог `src/` і запоўнены некалькімі асноўнымі файламі.

<div class="file-tree">
  <div class="item">src</div>
  <div class="children">
    <div class="item">app.controller.spec.ts</div>
    <div class="item">app.controller.ts</div>
    <div class="item">app.module.ts</div>
    <div class="item">app.service.ts</div>
    <div class="item">main.ts</div>
  </div>
</div>

Вось кароткі агляд гэтых асноўных файлаў:

|                          |                                                                                                                     |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| `app.controller.ts`      | Базавы кантролер з адным маршрутам.                                                                                 |
| `app.controller.spec.ts` | Модульныя тэсты для кантролера.                                                                                     |
| `app.module.ts`          | Каранёвы модуль прыкладання.                                                                                        |
| `app.service.ts`         | Базавая паслуга з дапамогай аднаго метаду.                                                                          |
| `main.ts`                | The entry file of the application which uses the core function `NestFactory` to create a Nest application instance. |

`main.ts` уключае асінхронную функцыю, якая будзе **запускаць** наша дадатак:

```typescript
@@filename(main)

import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
@@switch
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Каб стварыць асобнік прыкладання Nest, мы выкарыстоўваем асноўны клас `NestFactory` . `NestFactory` прапануе некалькі статычных метадаў, якія дазваляюць стварыць асобнік прыкладання. Метад `create()` вяртае аб'ект прыкладання, які выконвае інтэрфейс `INestApplication` . Гэты аб'ект забяспечвае набор метадаў, якія апісаны ў наступных раздзелах. У прыведзеным вышэй прыкладзе `main.ts` мы проста запускаем наш HTTP-слухач, які дазваляе прыкладанню чакаць ўваходных HTTP-запытаў.

Звярніце ўвагу, што праект, створаны з дапамогай Nest CLI, стварае першапачатковую структуру праекта, якая заахвочвае распрацоўшчыкаў прытрымлівацца правілаў захоўвання кожнага модуля ў сваім уласным спецыяльным каталогу.

:::info **Падказка** Па змаўчанні, калі пры стварэнні прыкладання ўзнікае якая-небудзь памылка, ваша прыкладанне выйдзе з кодам `1` . Калі вы хочаце, каб замест гэтага выдавалася памылка, адключыце опцыю `abortOnError` (напрыклад, `NestFactory.create(AppModule, {{ '{' }} abortOnError: false {{ '}' }})` . :::

<app-banner-courses></app-banner-courses>

## Платформа

Nest імкнецца быць фрэймворкам, які не залежыць ад платформы. Незалежнасць ад платформы дазваляе ствараць шматразовыя лагічныя часткі, якія распрацоўшчыкі могуць выкарыстоўваць у розных тыпах прыкладанняў. Тэхнічна Nest можа працаваць з любым фрэймворкам Node HTTP пасля стварэння адаптара. Існуюць дзве стандартныя платформы HTTP, якія падтрымліваюцца: [express](https://expressjs.com/) і [fastify](https://www.fastify.io) . Вы можаце выбраць той, які найбольш адпавядае вашым патрэбам.

|                    |                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `platform-express` | [Express](https://expressjs.com/) - добра вядомы мінімалістычны вэб-фреймворк для node. Гэта правераная ў баях, гатовая да вытворчасці бібліятэка з вялікай колькасцю рэсурсаў, укаранёных супольнасцю. Па змаўчанні выкарыстоўваецца пакет `@nestjs/platform-express` . Многія карыстальнікі добра абслугоўваюцца Express, і не трэба рабіць ніякіх дзеянняў, каб уключыць яго. |
| `platform-fastify` | [Fastify](https://www.fastify.io/) - гэта высокапрадукцыйная структура з нізкімі накладнымі выдаткамі, арыентаваная на забеспячэнне максімальнай эфектыўнасці і хуткасці. Пра тое, як ім карыстацца, чытайце [тут](/techniques/performance) .                                                                                                                                    |

Якая б платформа ні выкарыстоўвалася, яна адкрывае ўласны інтэрфейс прыкладання. Яны разглядаюцца адпаведна як `NestExpressApplication` і `NestFastifyApplication` .

Калі вы перадаеце тып у метад `NestFactory.create()` , як у прыкладзе ніжэй, аб'ект `app` будзе мець метады, даступныя выключна для гэтай канкрэтнай платформы. Аднак звярніце ўвагу, што вам не **трэба** ўказваць тып **, калі** вы сапраўды не хочаце атрымаць доступ да API базавай платформы.

```typescript
const app = await NestFactory.create<NestExpressApplication>(AppModule);
```

## Запуск прыкладання

Пасля завяршэння працэсу ўстаноўкі вы можаце выканаць наступную каманду ў камандным радку вашай АС, каб запусціць прыкладанне праслухоўванне ўваходных HTTP-запытаў:

```bash
$ npm run start
```

:::info **Падказка** Каб паскорыць працэс распрацоўкі (у 20 разоў хутчэйшыя зборкі), вы можаце выкарыстоўваць [канструктар SWC](/recipes/swc) , перадаўшы сцяг `-b swc` у скрыпт `start` наступным чынам: `npm run start -- -b swc` . :::

Гэтая каманда запускае праграму з HTTP-серверам, які праслухоўвае порт, вызначаны ў файле `src/main.ts` . Пасля запуску прыкладання адкрыйце браўзер і перайдзіце да `http://localhost:3000/` . Вы павінны ўбачыць `Hello World!` паведамленне.

Каб сачыць за зменамі ў вашых файлах, вы можаце выканаць наступную каманду, каб запусціць прыкладанне:

```bash
$ npm run start:dev
```

Гэтая каманда будзе сачыць за вашымі файламі, аўтаматычна перакампілюючы і перазагружаючы сервер.

## Лінтаванне і фарматаванне

[CLI](/cli/overview) забяспечвае максімум намаганняў для стварэння надзейнага працоўнага працэсу распрацоўкі ў маштабе. Такім чынам, згенераваны праект Nest пастаўляецца з прадусталяванымі праграмамі **расшыфроўкі** кода і **праграмай фарматавання** (адпаведна [eslint](https://eslint.org/) і [prettier](https://prettier.io/) ).

:::info **Падказка** Не ўпэўнены ў ролі фарматаў і лінтараў? Даведайцеся розніцу [тут](https://prettier.io/docs/en/comparison.html) . :::

Каб забяспечыць максімальную стабільнасць і пашыральнасць, мы выкарыстоўваем пакеты Base [`eslint`](https://www.npmjs.com/package/eslint) і [`prettier`](https://www.npmjs.com/package/prettier) cli. Такая ўстаноўка дазваляе акуратную інтэграцыю IDE з афіцыйнымі пашырэннямі.

Для асяроддзя без галавы, дзе IDE не мае значэння (бесперапынная інтэграцыя, перахваткі Git і г.д.), праект Nest пастаўляецца з гатовымі да выкарыстання сцэнарыямі `npm` .

```bash
# Lint and autofix with eslint
$ npm run lint

# Format with prettier
$ npm run format
```