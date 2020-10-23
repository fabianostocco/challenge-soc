Nesse arquivo contém as instruções para relizar o teste para a vaga na equipe de SOC na Zup.

### Índice
<!--ts-->
 * [Instruções](#instruções)</li>
 * [Resolução do Teste](#resolução-do-teste)</li>
 * [Resultados](#resultados)</li>
<!--te-->

---
### Instruções

Para teste você deverá:
```
Subir uma aplicacao web qualquer - CMS (wp,joomla,phpbb etc..)
```

O objetivo desse teste é monitorar todos serviço como CMS e o banco de dados, tanto as métricas quanto os logs dos container.


Os requisitos de monitoramento dessa infraestrutura são:

- Efetuar uma analise de vulnerabilidade no ambiente ( utilizando ferramentas de análise de vulnerabilidade do mercado ou qualquer uma opensource)
- Enviar todos logs para um concentrador de logs (utilizar a stack elk)
- monitorar todo ambiente com IDS/IPS (suricata ou snort ) 


O monitoramento dessa infraestrutura pode ser utilizando uma stack local como ELK ou Grafana com Prometheus ou utilizando alguma ferramenta SaaS (por exemplo, sydig ou NewRelic ou CloudWatch ou Elastic). Esperamos a solução na forma de script e documentação caso seja necessário o provisionamento da stack de monitoramento e a configuração do monitoramento das aplicações e banco de dados local. Caso seja uma ferramenta no modelo SaaS precisaremos de scripts que façam a configuração do monitoramento e documentação da utilização da ferramenta SaaS. É necessário realizar as seguintes tarefas no monitoramento da infraestrutura:

- Dashboard de monitoramento de métricas dos recursos das aplicações e do serviço de banco de dados;
- Dashboard para monitoramento das aplicações, podendo ser no modelo do APM ou busca de logs/erros via pesquisa (requer documentação caso os logs sejam via pesquisa**);
- Envio de alertas em caso de problemas;
- Use sua imaginação :)

**OBS**
- subir todo ambiente em container (swarm,k8s,docker-compose )
- salvar ambiente para replicação e avaliação
- 

**Use a seçcão [abaixo](#resolução-do-teste) para documentar a execução do seu teste ou apontar a documentação feita por você.**

---
### Resolução do Teste


---
### Resultados

Aceitaremos um fork deste repositório com suas alterações. Para isso, siga as instruções abaixo:

1. Clone o repositório localmente em seu computador:

   `git clone https://github.com/guilhermealbuquerquezup/challenge-soc.git`

2. Crie sua solução modificando e/ou criandos novos arquivos.

3. Crie o novo repositório no seu GitHub ou GitLab.

4. Clone o novo repositório localmente em seu computador:

   `git clone https://github.com/<usuario>/<nome-novo-repositorio>.git`

4. Adicione arquivos novos, caso os tenha criado.

   `git add .`

5. Commit local das suas modificações

   `git commit -am "<commit-message>"`

6. Gere um arquivo .patch com suas modificações locais

   `git push origin <nome-da-branch>`

7. Responda o e-mail anexando o link do repositório público.

**PS: O código ou documentação feita por você não será reutilizado por nós na Zup! :)**
