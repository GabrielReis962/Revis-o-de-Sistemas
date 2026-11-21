# ArenaXP

## Configuração do MySQL

O arquivo `src/main/resources/application.properties` já está configurado para:

- **Servidor:** `localhost:3306`
- **Banco de dados:** `arenaxp_db` (criado automaticamente, se necessário)
- **Usuário:** `root`
- **Senha:** definida na propriedade `spring.datasource.password` desse arquivo

Antes de executar a aplicação, confira essa propriedade e ajuste-a para a senha configurada no MySQL da máquina do avaliador. Se o usuário `root` não tiver senha, deixe o valor vazio:

```properties
spring.datasource.username=root
spring.datasource.password=
```

Se o MySQL usar outra senha, informe-a após o `=`. Se o usuário ou o endereço do servidor forem diferentes, ajuste também `spring.datasource.username` e `spring.datasource.url`.

Não compartilhe nem registre senhas reais no README ou no controle de versão.
