
```
> 🌐 Projeto TCC: Sistema Integrado de Monitoramento de Consumo de Água 🌐  

> 📅 Ano de Conclusão: 2023

> 👨‍💻 Desenvolvido por: Tiago Daltro Duarte

```

## 📖 **Sobre o Projeto**

Este projeto propõe uma solução inovadora para o **monitoramento de consumo de água residencial**. Com um dispositivo medidor e uma aplicação web integrados, o sistema permite que consumidores e concessionárias acompanhem dados de uso de água em tempo real, oferecendo uma visão precisa do consumo e automatizando a geração de faturas.

## 🚀 **Funcionalidades Principais**

- **Monitoramento de Consumo em Tempo Real**: 
  - Utilizando um **sensor de vazão YF-S201** e um **microcontrolador ESP32** com conectividade Wi-Fi 📶, o dispositivo mede continuamente o fluxo de água.
  - Os dados são transmitidos diretamente para o **Firebase** ☁️, onde ficam armazenados para consulta imediata pela aplicação web.

- **Aplicação Web de Gestão e Análise**:
  - Desenvolvida em **Python com o framework Django** 🐍, a aplicação web permite que os usuários da concessionárias acessem seu de consumo de água detalhado, incluindo o volume de água utilizado em cada residência.
  - A interface também permite visualizar **dados pessoais dos clientes** e **valor da fatura** de acordo com o consumo mensal.

- **Geração de Faturas Automática** 💳:
  - A partir dos dados coletados, o sistema calcula o valor a ser pago mensalmente com base no consumo registrado, proporcionando precisão e transparência na cobrança.

## 🔧 **Tecnologias e Ferramentas Utilizadas**

- **Dispositivo Medidor**:
  - **ESP32**: Microcontrolador com conectividade Wi-Fi para transmissão dos dados.
  - **Sensor YF-S201**: Responsável pela medição do fluxo de água 💦.
  
- **Back-end e Banco de Dados**:
  - **Firebase** ☁️: Armazenamento em tempo real para os dados de consumo de água.
  - **Python** e **Django** 🐍: Linguagem de programação e framework usados para desenvolvimento da aplicação web.

- **Hospedagem**:
  - **Amazon Web Services (AWS)** 🌐: A aplicação foi implementada na infraestrutura de computação em nuvem da AWS, garantindo escalabilidade e segurança.

## 🧪 **Processo de Testes**

Para validar a eficácia do sistema, o dispositivo foi instalado em um fluxo de água simulado, e as leituras foram monitoradas via aplicação web. Os dados de consumo foram atualizados em tempo real, e as faturas foram geradas automaticamente, confirmando a precisão e funcionalidade do sistema.


## 🏆 **Metodologia e Resultados Obtidos**


### 📸 **Código do Firmware e Monitor Serial**

Na figura é ilustrado um trecho do código do firmware do dispositivo de medição de consumo de água, juntamente com a ferramenta **Monitor Serial** disponibilizada no software ArduinoIDE. As mensagens de texto exibidas na figura foram enviadas pelo dispositivo de medição para logo mais serem enviadas para o Firebase e de lá para Aplicação Web. 👨‍💻💧

![Captura de tela do Monitor Serial](FOTOS_RESULTADOS/terceiro_litro.jpeg)

As mensagens mostradas indicam a leitura correta dos dados feita pelo dispositivo.


### 🧩 **Modelagem de Dados do Projeto**

O banco de dados elaborado possui quatro entidades: **cliente**, **fatura**, **endereço** e **administrador**.

- **Administrador**: A entidade **administrador** possui os atributos `login` e `senha`. Ela representa os administradores da plataforma web desenvolvida, que possuem acesso a todas as funcionalidades do sistema. 🔐

- **Cliente**: A entidade **cliente** possui os atributos `id_cliente`, `CPF`, `nome`, `nascimento`, `sexo`, `e-mail` e `telefone`. Ela representa os clientes da concessionária de água. 🚰 Não há cardinalidade entre a entidade **cliente** e a entidade **administrador**. No entanto, ao relacionar a entidade **cliente** com a entidade **endereço**, temos uma cardinalidade de (1, n), ou seja, um cliente pode ter no mínimo um endereço e no máximo vários endereços. 🏡

- **Endereço**: A entidade **endereço** possui os atributos `id_endereço`, `cidade`, `bairro`, `rua`, `número`, `complemento`, `cep`, `cliente`, `consumo_total`, `consumo_ultimo_mes` e representa os endereços dos clientes cadastrados. A cardinalidade da entidade **endereço** em relação à entidade **cliente** é de (1, 1), ou seja, um endereço só pode estar relacionado a um único cliente. Contudo, quando observamos a relação da entidade **endereço** com a entidade **fatura**, a cardinalidade é de (1, n), onde um endereço pode ter no mínimo uma fatura e no máximo várias faturas. 🏠💡

- **Fatura**: A entidade **fatura** possui os atributos `id_fatura`, `endereço`, `cliente`, `consumo_mensal`, `mes`, `ano`, `valor_pagar` e `fatura_paga`. A cardinalidade da entidade **fatura** em relação à entidade **endereço** é de (1, 1), ou seja, uma fatura só pode ter um único endereço. O atributo `consumo_mensal` representa o valor consumido de água por mês, e o atributo `valor_pagar` é o valor a ser pago pelo cliente. 💰💧


![Modelo Conceitual do Sistema](FOTOS_RESULTADOS/brModelo.JPG)



## 📡 **Envio de Dados para a Plataforma Firebase**

A cada novo litro consumido, o protótipo de medição envia o valor de consumo via **Wi-Fi** para a plataforma **Firebase**. 🌐💧 Dessa forma, o valor de consumo é persistido automaticamente no banco de dados criado na plataforma, sendo registrado no endereço composto por **CEP** e **número da residência**. 🏠🔢

Este endereço foi adicionado no **Firebase** de maneira automática assim que foi registrado pelo **administrador** na interface web. 🔐💻

Esse processo garante que o consumo de água de cada residência seja monitorado e armazenado em tempo real, proporcionando eficiência e precisão no controle de dados. 📊


![Dados de Consumo Persistidos no Firebase](FOTOS_RESULTADOS/FIREBASECONSUMO.JPG)


## Interface Web

### Login e Cadastro do Administrador da Aplicação

Na figura abaixo, temos a primeira página da interface já hospedada no **AWS Elastic Beanstalk** 🌐, a página de **login** 🔑, onde é possível digitar o **ID** e a **senha** do administrador já cadastrado no sistema, para acessar a página principal da aplicação. O próprio sistema foi desenvolvido para já possuir um **administrador chefe** 👨‍💼, criado quando o sistema é inicializado pela primeira vez, capaz de criar outros administradores.

![Login](FOTOS_RESULTADOS/LOGIN.JPG)

Caso um administrador da concessionária não esteja cadastrado, é possível clicar no botão **Cadastrar** ➕, e a tela de login do administrador será apresentada. Este acesso, no entanto, estará disponível somente para o **administrador chefe** 👨‍💼, que será responsável por cadastrar outros administradores.



![Login](FOTOS_RESULTADOS/paginaLOGINCADASTRO.JPG)


Na figura abaixo é representado a tela para cadastro de novos administradores:



![Login de Cadastro Administrador](FOTOS_RESULTADOS/CADASTRAR.JPG)




Na Figura abaixo é represtada a página principal da aplicação na aba clientes:



![Login de Cadastro Administrador](FOTOS_RESULTADOS/cliente.png)



Na Figura abaixo é represtada a página principal da aplicação na aba Endereço:



![Login de Cadastro Administrador](FOTOS_RESULTADOS/endereco.png)



Na Figura abaixo é represtada a página principal da aplicação na aba de Faturas:



![Login de Cadastro Administrador](FOTOS_RESULTADOS/fatura.png)


Para Clientes temos:

- Cadastrar Clientes:
   
  ![Login de Cadastro Administrador](FOTOS_RESULTADOS/CADASTRAR_CLIENTE.JPG)

- Listar Clientes

  ![Login de Cadastro Administrador](FOTOS_RESULTADOS/LISTAR_CLIENTE.JPG)

  - Dentro de Listar Clientes temos a visualização dos dados do cliente:

      ![Login de Cadastro Administrador](FOTOS_RESULTADOS/VISUALIZARDADOS_CLIENTE1.JPG)

      OBS: Os dados são apenas ilustrativos. Esses dados não existem!

Para Endereço temos:

- Novo Endereço

   ![Login de Cadastro Administrador](FOTOS_RESULTADOS/CADASTRAR_ENDERECO.JPG)

- Editar Endereço

  - 1ª Página
    
   ![Login de Cadastro Administrador](FOTOS_RESULTADOS/EDITAR_ENDERECO1.JPG)

  - 2ª Página
 
   ![Login de Cadastro Administrador](FOTOS_RESULTADOS/EDITAR_ENDERECO2.JPG)

- Excluir Endereço
  
  - 1ª Página
    
   ![Login de Cadastro Administrador](FOTOS_RESULTADOS/EXCLUIR_ENDERECO1.JPG)

   - 2ª Página

   ![Login de Cadastro Administrador](FOTOS_RESULTADOS/EXCLUIR_ENDERECO2.JPG)


  Para Faturas temos:

   - Listar Faturas
 
       - Sem Busca

         ![Login de Cadastro Administrador](FOTOS_RESULTADOS/Lista_de_Faturas.JPG)

      - Com Busca
    
        ![Login de Cadastro Administrador](FOTOS_RESULTADOS/FATURAS.JPG)


Concretização da implantação da aplicação no AWS:

  ![Login de Cadastro Administrador](FOTOS_RESULTADOS/ImplantouAmbienteAWS.JPG)


### 📊 **Conclusões**

- 📈 **Monitoramento Eficiente**: O dispositivo é capaz de registrar o consumo de água e enviar as informações à nuvem sem interrupções, oferecendo dados confiáveis.
- 📝 **Gestão Simplificada**: A aplicação web facilita a administração dos dados dos clientes e o cálculo de faturas, permitindo que concessionárias e consumidores acompanhem o uso de forma prática.
- 💡 **Conclusão**: O sistema desenvolvido se mostrou uma solução eficaz e prática para o monitoramento remoto do consumo de água, simplificando a gestão para concessionárias e promovendo o consumo consciente.

---

### 📂 **Estrutura do Repositório**

- [Device_code](https://github.com/Ti7801/SistemaIntegradoDeMonitoramentoDeConsumoDeAguaResidencial/tree/609e9c8fb474c2060b7c2885de116026bfcf6d58/CODIGO_PROTOTIPO_DE_MEDICAO/MONITORAMENTO_SENSOR_INTELIGENTE) 📟: Código e configurações para o ESP32 e o sensor de vazão YF-S201.
- [Aplicação Web](https://github.com/Ti7801/SistemaIntegradoDeMonitoramentoDeConsumoDeAguaResidencial/tree/609e9c8fb474c2060b7c2885de116026bfcf6d58/APLICACAO_WEB) 🌐: Código da aplicação web desenvolvida em Django.
- [Docs](https://repositorio.ifpb.edu.br/jspui/bitstream/177683/2926/1/Tiago%20Daltro%20Duarte%20-%20Sistema%20integrado%20de%20monitoramento%20de%20consumo%20de%20%C3%A1gua%20residencial%20-%20Copia.pdf) 📑: Documentação do projeto, incluindo especificações técnicas e relatórios de teste.

---

### 📞 **Contato**

Caso tenha interesse em saber mais sobre o projeto ou colaborar de alguma forma, fique à vontade para entrar em contato! 🚀

**E-mail**: [tiagodaltro19@gmail.com]  
**LinkedIn**: [https://www.linkedin.com/in/tiago-daltro-35241622a/]

---

