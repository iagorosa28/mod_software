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
| Identificador          | UC_01                                                          |
| :----------------------| :-----------------------------------------------------------------------------|
| Função                 | Verificar Cadastro                                     |
| Atores                 | Cliente, Atendente |
| Prioridade             | Essencial          |     
| Pré-condição           | Cliente precisa informar o código                                                          |
| Pós-condição           | Aprovação ou rejeição do cliente                                                                   |
| Fluxo Principal        | - O cliente informa seu código <br> - O atendente verifica se o cliente já possui cadastro (FS001, FS002) <br> |
| Fluxo Secundário FS001 | - Se o cliente não possuir cadastro, o atendente realiza o procedimento <br> |
| Fluxo Secundário FS002 | - Após confirmar o cadastro do cliente, o atendente verifica se há locações pendentes do cliente (FS003) <br> |
| Fluxo Secundário FS003 | - Caso o cliente tenha locações pendentes, o atendente deve recusar a locação <br> |

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
| Função          | Escolher categoria                                                                  |
| Atores          | Cliente                                                                             |
| Prioridade      | Essencial                                                                           |     
| Pré-condição    | Recepção do cliente na loja                                                         |
| Pós-condição    | O cliente avança para as etapas de pagamento e documentação                         |
| Fluxo Principal | - O cliente escolhe a categoria e o veículo que melhor atendem às suas preferências |

| Identificador   | UC_04                                                                                             |
| :---------------| :-------------------------------------------------------------------------------------------------|
| Função          | Pagar veículo                                                                                     |
| Atores          | Cliente, Sistem de pagamento                                                                      |
| Prioridade      | Essencial                                                                                         |     
| Pré-condição    | Escolha do veículo pelo cliente                                                                   |
| Pós-condição    | O cliente segue para os processos finais da locação do veículo                                    |
| Fluxo Principal | - O cliente realiza o pagamento da locação do veículo por meio de um sistema externo de pagamento |

| Identificador   | UC_05                                                          |
| :---------------| :-----------------------------------------------------------------------------|
| Função          | Alugar veículo                                     |
| Atores          | Cliente |
| Prioridade      | Essencial          |     
| Pré-condição    | Pagamento do veículo concluído                                                          |
| Pós-condição    | Veículo alugado com sucesso                                                                |
| Fluxo Principal | - O cliente só precisa finalizar a locação para ter seu veículo alugado <br> |

| Identificador   | UC_06                                                          |
| :---------------| :-----------------------------------------------------------------------------|
| Função          | Liberar veículo                                     |
| Atores          | Cliente, time do pátio |
| Prioridade      | Essencial          |     
| Pré-condição    | Locação do veículo finalizada com sucesso                                                          |
| Pós-condição    | O cliente pode utilizar o veículo alugado                                                                |
| Fluxo Principal | - A equipe do pátio libera o veículo para o cliente <br> |

| Identificador   | UC_07                                                          |
| :---------------| :-----------------------------------------------------------------------------|
| Função          | Verificar multas                                     |
| Atores          | Detran |
| Prioridade      | Essencial          |     
| Pré-condição    | Devolução do veículo pelo cliente concluída                                                          |
| Pós-condição    | Conclusão final da locação                                                                |
| Fluxo Principal | - O sistema consulta o Detran para verificar se há multas pendentes no veículo utilizado pelo cliente (FS004) <br> |
| Fluxo Secundário FS004 | - Caso existam multas pendentes relacionadas ao veículo do cliente, o sistema deve notificar e cobrar o cliente <br> |

## Diagrama de Classes

```mermaid
classDiagram
  CLIENTE "1" -- "1" LOCAÇÃO : REALIZA
  ATENDENTE "1" -- "1..*" CLIENTE : CADASTRA
  CLIENTE "1" -- "1" VEICULO : SOLICITA CATEGORIA
  VEICULO "1" -- "1" LOCAÇÃO : ATRIBUI MULTA  

  class VEICULO{
  - categoria string
  - modelo string
  - placa string
  + mostrarCategorias()
  + atribuirCategorias()
  + removerCategorias()
  }

  class ATENDENTE{
  - desempenho float
  - ocupação boolean
  + verificaDesempenho()
  + atualizarDesempenho()
  }

  class CLIENTE{
  - código string
  - locaçãoPendente boolean
  - cpf string
  - valorDeAluguel float
  - dataDeNascimento date
  - contadorDeLocaçãoMensal int
  - sequenciaMensal int
  - nivelCategoria int
  + cadastrar()
  + verificaCadastro()
  + atualizarLocaçõesPendentes()
  + registrarLocação()
  + verificarLocações()
  + registrarNívelDeCategoria()
  + verificarNívelDeCategoria()
  }

  class LOCAÇÃO{
  - multa float
  - valorDaLocação float
  - valorAdicional float
  - dataDeInicio date
  - dataDeEntrega date
  - reservaDeSegurança float
  + verificarMultas()
  + atribuirMultas()
  + atualizarValores()
  + registrarDatas()
  }


