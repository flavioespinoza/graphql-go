# graphql-go
his example shows how to implement a **TODO-app as a CLI tool** with Golang and Prisma.

## How to use

### 1. Download example & install dependencies

Clone the repository:

```bash
git clone https://github.com/flavioespinoza/graphql-go.git
```

Ensure dependencies are available and up-to-date:

```bash
cd prisma-examples/go/cli-app
dep ensure -update
```

### 2. Install the Prisma CLI

To run the example, you need the Prisma CLI. Please install it via Homebrew or [using another method](https://www.prisma.io/docs/prisma-cli-and-configuration/using-the-prisma-cli-alx4/#installation):

```bash
brew install prisma
brew tap
```

### 3. Set up database & deploy Prisma datamodel

For this example, you'll use a free _demo database_ (AWS Aurora) hosted in Prisma Cloud. To set up your database, run:

```bash
prisma deploy
```

Then, follow these steps in the interactive CLI wizard:

1. Select **Demo server**
1. **Authenticate** with Prisma Cloud in your browser (if necessary)
1. Back in your terminal, **confirm all suggested values**

<details>
 <summary>Alternative: Run Prisma locally via Docker</summary>

1. Ensure you have Docker installed on your machine. If not, you can get it from [here](https://store.docker.com/search?offering=community&type=edition).
1. Create `docker-compose.yml` for MySQL (see [here](https://www.prisma.io/docs/prisma-server/database-connector-POSTGRES-jgfr/) for Postgres):
    ```yml
    version: '3'
    services:
      prisma:
        image: prismagraphql/prisma:1.34
        restart: always
        ports:
        - "4466:4466"
        environment:
          PRISMA_CONFIG: |
            port: 4466
            databases:
              default:
                connector: mysql
                host: mysql
                port: 3306
                user: root
                password: prisma
                migrations: true
      mysql:
        image: mysql:5.7
        restart: always
        environment:
          MYSQL_ROOT_PASSWORD: prisma
        volumes:
          - mysql:/var/lib/mysql
    volumes:
      mysql:
    ```
1. Run `docker-compose up -d`
1. Set the `endpoint` in `prisma.yml` to `http://localhost:4466`
1. Run `prisma deploy`

</details>

You can now use [Prisma Admin](https://www.prisma.io/docs/prisma-admin/overview-el3e/) to view and edit your data by appending `/_admin` to your Prisma endpoint.

### 4. Use the CLI app

```bash
go run main.go
```

#### Add a `Todo` item

```bash
go run main.go create Groceries
```

#### List all `Todo` items

```bash
go run main.go list
```

#### Delete a `Todo` item

```bash
go run main.go delete Groceries
```

## Next steps

- [Use Prisma with an existing database](https://www.prisma.io/docs/-g003/)
- [Explore the Prisma client API](https://www.prisma.io/client/client-go)
- [Learn more about the GraphQL schema](https://www.prisma.io/blog/graphql-server-basics-the-schema-ac5e2950214e/)