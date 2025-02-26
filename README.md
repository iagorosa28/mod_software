# Modelagem de um sistema para uma locadora de veículos

> Status do projeto: Em andamento

> Este projeto nos foi proposto no 6º semestre na disciplina de Modelagem de Software Orientado a Objetos

> Escrevemos esse projeto juntos durante as aulas

### Tópicos

- [Apresentação](#apresentação)
- [Casos de uso](#casos-de-uso)
- [Diagrama de classes](#diagrama-de-classes)

### Dados temporários

Atores: cliente, atendente, time do pátio, operador, sistema do DETRAN

Classes: Veículo, funcionário, cliente, locação, "multas", 

## Apresentação 

## Casos de uso
### Diagrama de Casos de Uso

![DiagramaCasosDeUso drawio](https://github.com/user-attachments/assets/9d54e305-bb7f-4529-aa2e-add22c9c3915)

### Tabelas de Casos de Uso
| Identificador          | UC_01                                                                                                          |
| :----------------------| :--------------------------------------------------------------------------------------------------------------|
| Função                 | Verificar Cadastro                                                                                             |
| Atores                 | Cliente, Atendente                                                                                             |
| Prioridade             | Essencial                                                                                                      |     
| Pré-condição           | Cliente precisa informar o código                                                                              |
| Pós-condição           | Aprovação ou rejeição do cliente                                                                               |
| Fluxo Principal        | - O cliente informa seu código <br> - O atendente verifica se o cliente já possui cadastro (FS001, FS002) <br> |
| Fluxo Secundário FS001 | - Se o cliente não possuir cadastro, o atendente realiza o procedimento <br>                                   |
| Fluxo Secundário FS002 | - Após confirmar o cadastro do cliente, o atendente verifica se há locações pendentes do cliente (FS003) <br>  |
| Fluxo Secundário FS003 | - Caso o cliente tenha locações pendentes, o atendente deve recusar a locação <br>                             |

| Identificador   | UC_02                                                                                                                             |
| :---------------| :---------------------------------------------------------------------------------------------------------------------------------|
| Função          | Recepcionar na loja                                                                                                               |
| Atores          | Cliente, Atendente                                                                                                                |
| Prioridade      | Essencial                                                                                                                         |     
| Pré-condição    | Locação do cliente liberada                                                                                                       |
| Pós-condição    | O cliente pode selecionar o veículo de sua preferência                                                                            |
| Fluxo Principal | - Caso tanto o cadastro quanto as locações pendentes do cliente estejam em conformidade, o atendente recepciona o cliente na loja |

| Identificador   | UC_03                                                                               |
| :---------------| :-----------------------------------------------------------------------------------|
| Função          | Alugar veículo                                                                      |
| Atores          | Cliente                                                                             |
| Prioridade      | Essencial                                                                           |     
| Pré-condição    | Recepção do cliente na loja                                                         |
| Pós-condição    | Pagar veículo                                                                       |
| Fluxo Principal | - O cliente escolhe a categoria e o veículo que melhor atendem às suas preferências |

| Identificador   | UC_04                                                                                             |
| :---------------| :-------------------------------------------------------------------------------------------------|
| Função          | Pagar veículo                                                                                     |
| Atores          | Cliente, Sistem de pagamento                                                                      |
| Prioridade      | Essencial                                                                                         |     
| Pré-condição    | Escolha do veículo pelo cliente                                                                   |
| Pós-condição    | Liberação do veículo                                                                              |
| Fluxo Principal | - O cliente realiza o pagamento da locação do veículo por meio de um sistema externo de pagamento |

| Identificador   | UC_05                                               |
| :---------------| :---------------------------------------------------|
| Função          | Liberar veículo                                     |
| Atores          | Cliente, time do pátio                              |
| Prioridade      | Essencial                                           |     
| Pré-condição    | Locação do veículo finalizada com sucesso           |
| Pós-condição    | O cliente pode utilizar o veículo alugado           |
| Fluxo Principal | - A equipe do pátio libera o veículo para o cliente |

| Identificador          | UC_06                                                          |
| :----------------------| :-----------------------------------------------------------------------------|
| Função                 | Verificar multas                                     |
| Atores                 | Detran |
| Prioridade             | Essencial          |     
| Pré-condição           | Devolução do veículo pelo cliente concluída                                                          |
| Pós-condição           | Conclusão final da locação                                                                |
| Fluxo Principal        | - O sistema consulta o Detran para verificar se há multas pendentes no veículo utilizado pelo cliente (FS004) <br> |
| Fluxo Secundário FS004 | - Caso existam multas pendentes relacionadas ao veículo do cliente, o sistema deve notificar e cobrar o cliente <br> |

## Diagrama de Classes

```mermaid
classDiagram
  Pessoa <-- Cliente
  Pessoa <-- Funcionario
  Funcionario "1" -- "0..*" Cliente : Cadastra
  Funcionario "1" -- "0..*" Locacao : Libera
  Cliente "1" -- "1" Locacao : Realiza
  Cliente "1" -- "1" Veiculo : Aluga
  Cliente "1" -- "1" Historico : Tem
  Historico "1" -- "1" Locacao : Pertence
  Historico "1" -- "0..*" Multa : Registra
  Veiculo "1" -- "1" Locacao : Pertence
  Veiculo "1" -- "0..*" Multa : Leva

  class Pessoa{
  - cpf string
  - dataDeNascimento date
  - nome string
  }

  class Cliente{
  - codigo string
  - nivelCategoria int
  + cadastrar()
  + verificarCadastro()
  + atualizarNivelCategoria()
  + verificarNivelCategoria()
  }

  class Funcionario{
  - desempenho float
  - ocupacao boolean
  - tipoFuncionario string
  + atualizarDesempenho()
  + verificarDesempenho()
  }

  class Historico{
  - multasAtivas boolean
  - locacaoPendente boolean
  - sequenciaLocacao int
  + consultarHistorico()
  }

  class Locacao{
  - valorLocacao float
  - valorAdicional float
  - dataInicio date
  - dataEntrega date
  - reservaSeguranca
  + atualizarValores()
  + registrarDatas()
  }

  class Veiculo{
  - categoria string
  - modelo string
  - placa string
  + registrarVeiculo()
  + mostrarInformacoes()
  + removerVeiculo()
  }

  class Multa{
  - tipoMulta string
  - valorMulta float
  - dataMulta date
  + registrarMulta()
  }
```
