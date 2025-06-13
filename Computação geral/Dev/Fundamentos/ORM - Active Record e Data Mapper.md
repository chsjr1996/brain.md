#orm #activerecord #datamapper #oop

Existem duas opções comuns de ORM que são a Active Record e Data Mapper, cada *framework* geralmente opta por usar ou uma, ou outra abordagem.

Por exemplo, o Laravel utiliza o padrão Active Record, já o Symfony Framework utiliza o padrão Data Mapper.

## Active Record características
Normalmente esse padrão é mais fácil de se trabalhar, por dispor de recursos que facilitam a gestão dos dados através de abstrações presentes nos *frameworks* que o implementam. 

Porém, isso tem um custo de ambiguidade entre a lógica de registro e a lógica de objeto, e apesar das abstrações facilitarem a gestão, pode ser complicado de se entender o funcionamento interno, e em alguns casos modificá-lo pode não ser tão simples.

Outras características são:
- Uma classe/objeto (model) de registro representa uma linha/registro no banco de dados;
- Este objeto pode conter regras de negócio baseados no que ele modela;
- Este objeto pode dispor de métodos com funcionalidades de armazenamento, permitindo salvar a si mesmo (update);
- Os _models_ são fortemente acoplados à camada de acesso aos dados;
- Define suas próprias convenções e expressões idiomáticas;

## Data Mapper características
Sua implementação existe um maior cuidado, já que as definições de cada model deve ser feita por "completa", o que torna o código mais verbose em certo ponto.

Porém, as abstrações aqui podem ser aplicadas diretamente pelo desenvolvedor, o que pode facilitar o entendimento do funcionamento, bem como sua manutenção`*`.

Outras características são:
- Uma classe/objeto (entity) somente modela o que essa informação representa na aplicação;
- Depende de uma classe de serviço para realizar a gestão, normalmente denominadas de *repository*;
- Possibilita a separação de conceitos (SoC), facilitando a modularização;
- Permite uso mais idiomático da linguagem de domínio (útil para DDD);
- `*` Depende de experiência do desenvolvedor devido a complexidade;

## Conclusão
No _Active Record_ o _model_ está fortemente acoplado ao banco de dados, possibilitando que operações sejam realizadas diretamente no objeto, como salvar ou atualizar alguma informação. Aqui temos uma abordagem mais dinâmica, e que fica mais sob controle do _framework_.

No _Data Mapper_ a _entity_ está desacoplada do banco de dados, dependendo de uma camada extra de serviço para realizara as operações de alterações de dados, tarefa esta que é delegada ao _repository_. Aqui temos uma abordagem mais manual, e que fica sob controle do código desenvolvido.

Portanto, a escolha de cada padrão vai depender do _framework_ escolhido, reforçando que o _Data Mapper_ tende ser mais complexo, porém mais flexível e ideal para aplicações que dependem de uma arquitetura DDD, como micro serviços por exemplo.

Enquanto o _Active Record_ pode ser uma boa escolha para aplicações monolíticas, ou de escalamento vertical.

---
## Referências
- [Medium - Entenda ORM: Active Record e Data Mapper (Matheus Flauzino)]()