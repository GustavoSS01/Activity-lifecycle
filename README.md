# Activity-lifecycle por Gustavo dos Santos Silva, ADS - 4° Período

# Introdução

O ciclo de vida de uma Activity em Android é um conceito fundamental para o desenvolvimento de aplicativos móveis. Ele define como a Activity responde a eventos do sistema e interações do usuário, garantindo uma gestão eficiente de recursos e uma experiência de usuário fluida. Este trabalho aborda os principais callbacks do ciclo de vida da Activity, explicando suas funções e interações, conforme mostrado na figura abaixo.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/d865c2d4-9ce8-4556-9f84-77ca7a20666b)

# 1. Activity Launched
Quando uma Activity é iniciada, o sistema chama uma série de métodos de callback que configuram a interface do usuário e iniciam a lógica da aplicação.

# 1.1 onCreate()
Descrição: Esse callback precisa ser implementado. Ele é acionado assim que o sistema cria a Activity. Quando a Activity é criada, ela insere o estado Created. No método onCreate(), execute a lógica básica de inicialização do aplicativo que acontece apenas uma vez durante toda a vida útil da Activity. 
<br/>
Uso:  A implementação de onCreate() pode vincular dados a listas, associar a Activity a um ViewModel e instanciar algumas variáveis com escopo de classe. Esse método recebe o parâmetro savedInstanceState, sendo um objeto Bundle que contém o estado salvo anteriormente da Activity. Se a Activity nunca existiu, o valor do objeto Bundle será nulo.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/61a661a3-c517-4b49-8c10-4734f2857a28)

# 1.2 onStart()
Descrição: Quando a Activity entra no estado Iniciado, o sistema invoca onStart(). Essa chamada torna a Activity visível para o usuário enquanto o aplicativo se prepara para a Activity entrar em primeiro plano e se torne interativa.<br/>
Uso: Preparar a Activity para entrar em cena.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/74097d75-d137-4b84-8bde-24cb7b5b177d)

# 1.3 onResume()
Descrição: Quando uma Activity entra no estado "Resume", ela vai para o primeiro plano e o sistema chama o retorno de chamada onResume(). É neste estado que a aplicação interage com o usuário. Nesse estado, a Activity está no topo da pilha de Activitys e o usuário pode interagir com ela. 
Quaisquer componentes com reconhecimento de ciclo de vida vinculados ao ciclo de vida da Activity recebem o evento ON_RESUME quando a Activity passa para o estado "Retomar". Neste ponto, o componente do ciclo de vida pode ativar qualquer funcionalidade que precise ser operada enquanto o componente estiver visível e em primeiro plano;
Quando ocorre um evento de interrupção, a Activity entra no estado "pausado" e o sistema chama o retorno de chamada onPause().
<br/>
Uso:Iniciar animações, tocar música, abrir conexões exclusivas e similares.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/8cdabf1d-3125-4bde-80eb-c9b98fd4fe13)


# 2. Activity Running 
Quando a Activity está em execução (Activity running), ela está no estado no qual o usuário pode interagir com ela.

# 2.1 onPause()
Descrição: O sistema chama esse método como o primeiro indício de que o usuário está saindo da Activity, embora nem sempre isso signifique que a Activity vai ser destruída. Isso indica que a Activity não está mais em primeiro plano, mas ainda estará visível se o usuário estiver no modo de várias janelas. Há vários motivos para uma Activity entrar nesse estado:
  - Um evento que interrompe a execução do app, pausa a Activity atual. Esse é o caso mais comum.
  - No modo de várias janelas, apenas um app fica em foco por vez, e o sistema pausa todos os outros.
  - A abertura de uma nova Activity semitransparente, como uma caixa de diálogo, pausa a Activity que ela abrange. Enquanto a Activity estiver parcialmente visível, mas não for o foco, ela permanecerá pausada.
<br/>

Uso: Pausar animações ou outros processos que consomem CPU.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/213eee6c-6d1e-4e0b-a1c8-0607bbb6964d)


# 2.2 onStop()
Descrição: Quando uma Activity transita para um estado "Interrompido", cada componente com reconhecimento de ciclo de vida associado ao ciclo de vida da Activity recebe um evento ON_STOP. É quando um componente do ciclo de vida pode interromper funções que não precisam ser executadas enquanto não estiver visível na tela. Quando a Activity é movida para o estado "Interrompido", qualquer componente com reconhecimento de ciclo de vida vinculado ao ciclo de vida da Activity recebe o evento ON_STOP. É nesse momento que os componentes do ciclo de vida podem interromper qualquer funcionalidade que não precise operar enquanto o componente não estiver visível na tela.
A partir do estado "Interrompido", a Activity volta a interagir com o usuário ou para de operar e é encerrada. Se a Activity voltar, o sistema invocará onRestart(). Caso a Activity deixe de operar, o sistema chamará onDestroy().
<br/>
Uso: Liberar recursos que não são necessários enquanto a Activity não está visível, como parar serviços ou desativar sensores.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/cb975101-2d83-4a4b-b035-e2819d858cba)


# 2.3 onDestroy()
Descrição: onDestroy() é chamado antes de a Activity ser destruída. O sistema invoca esse callback por um destes dois motivos:
- A Activity está sendo concluída porque o usuário descartou completamente a Activity ou porque finish() está sendo chamado na Activity.
- O sistema está destruindo temporariamente a Activity devido a uma mudança na configuração, como a rotação do dispositivo ou a entrada no modo de várias janelas.
<br/>
Quando a Activity é movida para o estado destruído, qualquer componente ciente do ciclo de vida vinculado ao ciclo de vida da Activity recebe o evento ON_DESTROY. É nesse momento que os componentes do ciclo de vida podem limpar tudo o que precisam antes que o Activity seja destruído.
<br/>
Uso: Fazer a limpeza final de recursos.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/15e654d1-c9a9-4537-82b9-912dbf2d665c)

# 3. Retorno e Navegação

# 3.1 onRestart()
Descrição: Chamado depois que a Activity foi parada, antes de ser iniciada novamente. Ele indica que a Activity está voltando para interagir com o usuário.
<br/>
Uso: Restaurar o estado da Activity de forma que possa ser retomada com uma transição suave.

![image](https://github.com/GustavoSS01/Activity-lifecycle/assets/69322864/b7ae9946-69ae-4fa9-a0c1-eca7cae445b5)

# 3.2 Navegação para outra Activity
Quando o usuário navega para outra Activity, o sistema pode chamar onPause() e onStop(), dependendo de como a nova Activity é lançada.

# Conclusão
O ciclo de vida de uma Activity no Android é um processo complexo que permite aos desenvolvedores gerenciar eficientemente os recursos do aplicativo e garantir uma experiência de usuário otimizada. Entender cada um desses callbacks e como utilizá-los adequadamente é crucial para o desenvolvimento de aplicativos Android robustos e eficientes.

# Referências
The Activity Lifecycle - Android Devs
https://developer.android.com/guide/components/activities/activity-lifecycle
