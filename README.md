# Projeto realizado para o Trabalho de Conclusão de Curso de Engenharia Elétrica no Instituto Federal da Paraíba.


### O sistema integrado consiste em um dispositivo medidor de consumo de água, que deve ser instalado nas residncias dos clientes da concessionária, e uma aplicação web capaz de gerenciar e apresentar esses dados de consumo. Além disso, são apresentados os dados pessoais de cada cliente e o valor a ser pago mensalmente pelo consumo de água em litros. Para a construção do dispositivo de medição foram utilizados o microcontrolador ESP32 que possui conectividade WI-FI e o sensor de vazão YF-S201. As medições de consumo realizadas pelo dispositivo são enviadas para o banco de dados em tempo real da nuvem Firebase, que hospeda os dados de consumo de todas as residncias até que sejam lidos pela aplicação web desenvolvida. A aplicação foi implementada com a linguagem de programação Python e o framework Django. Após implementação, ela foi hospedada nos serviços de computação em nuvem Amazon Web Services (AWS). Para a realização dos testes, o dispositivo desenvolvido foi instalado em um Ćuxo de água e veriĄcou-se na aplicação web os dados de consumo e a geração das faturas referentes ao consumo medido. Com base nos resultados obtidos, conclui-se que o sistema desenvolvido é capaz de monitorar remotamente o consumo de água, gerenciar os dados pessoais dos clientes e computar suas faturas.
