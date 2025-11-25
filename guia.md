meu bloco de notas do artigo – como eu escrevo mesmo, sem frescura
ja baixei o opendss e o 8500 node ta aqui na pasta
vou usar o 8500 mas só um ramal bem fdp daqueles bem longos pra ficar realista pra caralho, tipo rede rural da bahia mesmo
fase 1 – arrumar a casa

opendss instalado (ja ta)
8500 node baixado, ta na pasta IEEE_8500
peguei o perfil solar real da bahia no labren/ccst, vou jogar no loadshape pra parar de usar aquele dummy ridiculo
reli a proposta final pra não esquecer o que eu prometi kkk

fase 2 – meter a cara no modelo

rodar o 8500 original pra ver qual ramal é o pior (o mais longo, maior queda de tensão, aquele que parece rede de interior)
escolher uma barra lá na ponta desse ramal e colar minha carga de irrigação (aquela de 750kVA que eu já tenho pronta)
obs: o 8500 é 4.16kV em alguns trechos, vou ter que ajustar a tensão da minha carga se não queimar tudo
colocar o PV (2MW que eu já tenho no PVSystem.dss) perto da irrigação
colocar o storage do lado também (ainda to decidindo kVA/kWh)
fazer um Master_novo.dss que:
chama o Master original do 8500
depois chama meus arquivos: LoadShapes_novo.dss, Loads_irrigacao.dss, PVSystem.dss, Storage.dss

(talvez) mudar a carga de irrigação pra model=8 (motor de indução) pra simular partida pesada e afundamento brabo

fase 3 – rodar as simulações
cenário 1 – base: sem pv sem storage → daily mode → ver Vmin e perdas no ramal
cenário 2 – só irrigação ligando: fault study perto da barra pra ver o sag quando o motor parte
cenário 3 – com pv ligado → daily → ver elevação de tensão no meio do dia
cenário 4 – pv + storage com controller → daily → ver se o storage segura o sag e corta o overvoltage
cenário extra – ficar variando tamanho do storage e %discharge do controller até achar o ponto doce
vou usar monitor em tudo, exportar csv e jogar no python depois pra fazer gráfico bonito
fase 4 – escrever essa porra
introdução → falar que 8500 é perfeito porque tem ramal ruralzão, longa distância, baixa densidade
metodologia → explicar que peguei só o ramal crítico pra focar no pior caso (justificar)
resultados → gráficos dos 4 cenários, antes/depois, sag mitigado, tensão regulada
discussão → storage resolve mesmo, custo x benefício, etc
conclusão → deu certo, artigo pronto, vou dormir


https://labren.ccst.inpe.br/atlas_2017_BA.html
ue inferno de computador
