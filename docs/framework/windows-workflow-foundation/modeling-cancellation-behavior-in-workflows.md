---
title: "Modellieren des Abbruchverhaltens in Workflows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d48f6cf3-cdde-4dd3-8265-a665acf32a03
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Modellieren des Abbruchverhaltens in Workflows
Aktivitäten können innerhalb eines Workflows abgebrochen werden, z. B. durch eine <xref:System.Activities.Statements.Parallel>\-Aktivität, die unvollständige Verzweigungen abbricht, wenn ihre <xref:System.Activities.Statements.Parallel.CompletionCondition%2A>`true` ergibt, oder von außerhalb des Workflows, wenn der Host <xref:System.Activities.WorkflowApplication.Cancel%2A> aufruft.Workflowautoren können die Abbruchbehandlung mithilfe der <xref:System.Activities.Statements.CancellationScope>\-Aktivität oder der <xref:System.Activities.Statements.CompensableActivity>\-Aktivität bereitstellen oder können benutzerdefinierte Aktivitäten erstellen, die eine Abbruchlogik bereitstellen.Dieses Thema bietet eine Übersicht über den Abbruch in Workflows.  
  
## Abbruch, Kompensation und Transaktionen  
 Wenn Sie Transaktionen verwenden, kann Ihre Anwendung alle Änderungen zurücknehmen \(Rollback\), die innerhalb der Transaktion ausgeführt wurden, falls während des Transaktionsprozesses ein Fehler auftritt.Möglicherweise ist jedoch nicht die gesamte Arbeit, die abgebrochen oder rückgängig gemacht werden muss, für Transaktionen geeignet, beispielsweise Prozesse mit langer Laufzeit oder Aufgaben, die keine Transaktionsressourcen einschließen.Die Kompensation stellt ein Modell zum Rückgängigmachen von zuvor abgeschlossenen, nicht transaktionalen Aufgaben bereit, wenn im Workflow ein nachfolgender Fehler auftritt.Der Abbruch stellt ein Modell für Workflow\- und Aktivitätsautoren zum Behandeln von nicht transaktionalen Aufgaben bereit, die noch nicht abgeschlossen waren.Wenn die Ausführung einer Aktivität nicht abgeschlossen war und abgebrochen wird, wird die Abbruchlogik aufgerufen, falls verfügbar.  
  
> [!NOTE]
>  [!INCLUDE[crabout](../../../includes/crabout-md.md)] zu Transaktionen und Kompensation finden Sie unter [Transaktionen](../../../docs/framework/windows-workflow-foundation//workflow-transactions.md) und [Kompensierung](../../../docs/framework/windows-workflow-foundation//compensation.md).  
  
## Verwenden von CancellationScope  
 Die <xref:System.Activities.Statements.CancellationScope>\-Aktivität verfügt über zwei Abschnitte, die untergeordnete Aktivitäten enthalten können: <xref:System.Activities.Statements.CancellationScope.Body%2A> und <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>.Im <xref:System.Activities.Statements.CancellationScope.Body%2A> befinden sich die Aktivitäten, aus denen die Logik der Aktivität besteht, und im <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> befinden sich die Aktivitäten, die die Abbruchlogik für die Aktivität bereitstellen.Eine Aktivität kann nur abgebrochen werden, wenn sie noch nicht abgeschlossen wurde.Im Fall der <xref:System.Activities.Statements.CancellationScope>\-Aktivität verweist der Abschluss auf den Abschluss der Aktivitäten im <xref:System.Activities.Statements.CancellationScope.Body%2A>.Wenn eine Abbruchanforderung geplant ist und die Aktivitäten im <xref:System.Activities.Statements.CancellationScope.Body%2A> nicht abgeschlossen wurden, dann wird der <xref:System.Activities.Statements.CancellationScope> als <xref:System.Activities.ActivityInstanceState> markiert, und die <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>\-Aktivitäten werden ausgeführt.  
  
### Abbrechen eines Workflows vom Host aus  
 Ein Host kann einen Workflow abbrechen, indem er die <xref:System.Activities.WorkflowApplication.Cancel%2A>\-Methode der <xref:System.Activities.WorkflowApplication>\-Instanz aufruft, die den Workflow hostet.Im folgenden Beispiel wird ein Workflow erstellt, der einen <xref:System.Activities.Statements.CancellationScope> aufweist.Der Workflow wird aufgerufen und anschließend ruft der Host <xref:System.Activities.WorkflowApplication.Cancel%2A> auf.Die Hauptausführung des Workflows wird beendet, der <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> des <xref:System.Activities.Statements.CancellationScope> wird aufgerufen, und dann wird der Workflow mit einem Status von <xref:System.Activities.ActivityInstanceState> abgeschlossen.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#35](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#35)]  
  
 Wenn dieser Workflow aufgerufen wird, wird die folgende Ausgabe in der Konsole angezeigt.  
  
 **Starten des Workflows.**   
**CancellationHandler aufgerufen.**   
**Workflow b30ebb30\-df46\-4d90\-a211\-e31c38d8db3c abgebrochen.**    
> [!NOTE]
>  Wenn eine <xref:System.Activities.Statements.CancellationScope>\-Aktivität abgebrochen und der <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> aufgerufen wird, liegt es in der Verantwortung des Workflowautors, den Status der abgebrochenen Aktivität vor dem Abbruch zu bestimmen, um die entsprechende Abbruchlogik bereitzustellen.Der <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> stellt keine Informationen zum Status der abgebrochenen Aktivität bereit.  
  
 Ein Workflow kann auch vom Host abgebrochen werden, wenn eine nicht behandelte Ausnahme nach dem Stamm des Workflows ausgelöst wird und der <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>\-Handler <xref:System.Activities.UnhandledExceptionAction> zurückgibt.In diesem Beispiel startet der Workflow und löst dann eine <xref:System.ApplicationException> aus.Diese Ausnahme wird vom Workflow nicht behandelt, daher wird der <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>\-Handler aufgerufen.Der Handler weist die Laufzeit an, den Workflow abzubrechen, und der <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> der derzeit ausgeführten <xref:System.Activities.Statements.CancellationScope>\-Aktivität wird aufgerufen.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#36](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#36)]  
  
 Wenn dieser Workflow aufgerufen wird, wird die folgende Ausgabe in der Konsole angezeigt.  
  
 **Starten des Workflows.**   
**OnUnhandledException in Workflow 6bb2d5d6\-f49a\-4c6d\-a988\-478afb86dbe9**   
**Eine ApplicationException wurde ausgelöst.**   
**CancellationHandler aufgerufen.**   
**Workflow 6bb2d5d6\-f49a\-4c6d\-a988\-478afb86dbe9 abgebrochen.**    
### Abbrechen einer Aktivität innerhalb eines Workflows  
 Eine Aktivität kann auch von ihrem übergeordneten Element abgebrochen werden.Wenn eine <xref:System.Activities.Statements.Parallel>\-Aktivität beispielsweise über mehrere ausgeführte Verzweigungen verfügt, und ihre <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> ergibt `true`, werden ihre unvollständigen Verzweigungen abgebrochen.In diesem Beispiel wird eine <xref:System.Activities.Statements.Parallel>\-Aktivität erstellt, das zwei Verzweigungen aufweist.Ihre <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> ist auf `true` festgelegt, damit die <xref:System.Activities.Statements.Parallel> abgeschlossen wird, sobald die einzelnen Verzweigungen abgeschlossen sind.In diesem Beispiel wird Verzweigung 2 abgeschlossen, daher wird Verzweigung 1 abgebrochen.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#37](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#37)]  
  
 Wenn dieser Workflow aufgerufen wird, wird die folgende Ausgabe in der Konsole angezeigt.  
  
 **Starten von Verzweigung 1.**   
**Verzweigung 2 abgeschlossen.**   
**Verzweigung 1 abgebrochen.**   
**Workflow e0685e24\-18ef\-4a47\-acf3\-5c638732f3be abgeschlossen.**  Aktivitäten werden auch abgebrochen, wenn eine Ausnahme nach den Stamm der Aktivität ausgelöst wird, jedoch auf einer höheren Ebene im Workflow behandelt wird.In diesem Beispiel besteht die Hauptlogik des Workflows aus einer <xref:System.Activities.Statements.Sequence>\-Aktivität.Die <xref:System.Activities.Statements.Sequence> wird als <xref:System.Activities.Statements.CancellationScope.Body%2A> einer <xref:System.Activities.Statements.CancellationScope>\-Aktivität angegeben, die in einer <xref:System.Activities.Statements.TryCatch>\-Aktivität enthalten ist.Aus dem Text der <xref:System.Activities.Statements.Sequence> wird eine Ausnahme ausgelöst, die von der übergeordneten <xref:System.Activities.Statements.TryCatch>\-Aktivität behandelt wird, und die <xref:System.Activities.Statements.Sequence> wird abgebrochen.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#39](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#39)]  
  
 Wenn dieser Workflow aufgerufen wird, wird die folgende Ausgabe in der Konsole angezeigt.  
  
 **Starten der Sequenz.**   
**Sequenz abgebrochen.**   
**Ausnahme abgefangen.**   
**Workflow e3c18939\-121e\-4c43\-af1c\-ba1ce977ce55 abgeschlossen.**   
### Auslösen von Ausnahmen von einem CancellationHandler aus  
 Alle vom <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> eines <xref:System.Activities.Statements.CancellationScope> ausgelösten Ausnahmen haben schwerwiegende Auswirkungen auf den Workflow.Wenn für Ausnahmen die Möglichkeit besteht, einen <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> zu umgehen, verwenden Sie im <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A><xref:System.Activities.Statements.TryCatch>, um diese Ausnahmen abzufangen und zu behandeln.  
  
### Abbruch mithilfe von CompensableActivity  
 Genau wie die <xref:System.Activities.Statements.CancellationScope>\-Aktivität verfügt die <xref:System.Activities.Statements.CompensableActivity> über einen <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>.Wenn eine <xref:System.Activities.Statements.CompensableActivity> abgebrochen wird, werden alle Aktivitäten in ihrem <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> aufgerufen.Dies kann nützlich für das Rückgängigmachen teilweise abgeschlossener Arbeit sein.Weitere Informationen zur Verwendung von <xref:System.Activities.Statements.CompensableActivity> für die Kompensation und den Abbruch finden Sie unter [Kompensierung](../../../docs/framework/windows-workflow-foundation//compensation.md).  
  
## Abbruch mithilfe von benutzerdefinierten Aktivitäten  
 Für Autoren von benutzerdefinierten Aktivitäten gibt es mehrere Möglichkeiten, eine Abbruchlogik in ihre benutzerdefinierten Aktivitäten zu implementieren.Benutzerdefinierte Aktivitäten, die von <xref:System.Activities.Activity> abgeleitet werden, können Abbruchlogik implementieren, indem <xref:System.Activities.Statements.CancellationScope> oder eine andere benutzerdefinierte Aktivität, die Abbruchlogik enthält, in den Text der Aktivität eingefügt wird.Von <xref:System.Activities.AsyncCodeActivity> und <xref:System.Activities.NativeActivity> abgeleitete Aktivitäten können ihre jeweilige <xref:System.Activities.NativeActivity.Cancel%2A>\-Methode überschreiben und an dieser Stelle eine Abbruchlogik bereitstellen.Von <xref:System.Activities.CodeActivity> abgeleitete Aktivitäten stellen keine Möglichkeit zum Abbruch dar, da die gesamte Arbeit in einer einzigen Ausführung ausgeführt wird, wenn die Laufzeit die <xref:System.Activities.CodeActivity.Execute%2A>\-Methode aufruft.Wenn die execute\-Methode noch nicht aufgerufen wurde und eine auf <xref:System.Activities.CodeActivity> basierende Aktivität abgebrochen wird, wird die Aktivität mit einem Status von <xref:System.Activities.ActivityInstanceState> geschlossen, und die <xref:System.Activities.CodeActivity.Execute%2A>\-Methode wird nicht aufgerufen.  
  
### Abbruch mithilfe von NativeActivity  
 Von <xref:System.Activities.NativeActivity> abgeleitete Aktivitäten können die <xref:System.Activities.NativeActivity.Cancel%2A>\-Methode überschreiben, um eine benutzerdefinierte Abbruchlogik bereitzustellen.Wenn diese Methode nicht überschrieben wird, dann wird die standardmäßige Workflowabbruchlogik angewendet.Bei einem standardmäßigen Abbruch handelt es sich um den Prozess, der für eine <xref:System.Activities.NativeActivity> auftritt, die die <xref:System.Activities.NativeActivity.Cancel%2A>\-Methode nicht überschreibt oder dessen <xref:System.Activities.NativeActivity.Cancel%2A>\-Methode die <xref:System.Activities.NativeActivity> <xref:System.Activities.NativeActivity.Cancel%2A>\-Basismethode aufruft.Wenn eine Aktivität abgebrochen wird, kennzeichnet die Laufzeit die Aktivität für den Abbruch und behandelt automatisch eine bestimmte Bereinigung.Wenn die Aktivität nur über ausstehende Lesezeichen verfügt, werden die Lesezeichen entfernt, und die Aktivität wird als <xref:System.Activities.ActivityInstanceState> markiert.Alle ausstehenden untergeordneten Aktivitäten in der abgebrochenen Aktivität werden dann abgebrochen.Jeder Versuch zur Planung zusätzlicher untergeordneter Aktivitäten wird ignoriert wird, und die Aktivität wird als <xref:System.Activities.ActivityInstanceState> markiert.Wenn eine ausstehende untergeordnete Aktivität im Zustand <xref:System.Activities.ActivityInstanceState> oder <xref:System.Activities.ActivityInstanceState> abgeschlossen wird, wird die Aktivität als <xref:System.Activities.ActivityInstanceState> markiert.Beachten Sie, dass eine Abbruchanforderung ignoriert werden kann.Wenn eine Aktivität nicht über ausstehende Lesezeichen oder ausgeführte untergeordnete Aktivitäten verfügt und keine zusätzlichen Arbeitsaufgaben plant, nachdem sie für einen Abbruch gekennzeichnet wurde, wird sie erfolgreich abgeschlossen.Dieser standardmäßige Abbruch ist für viele Szenarien ausreichen, wenn jedoch eine zusätzliche Abbruchlogik erforderlich ist, können die integrierten Abbruchaktivitäten oder benutzerdefinierte Aktivitäten verwendet werden.  
  
 Im folgenden Beispiel ist die <xref:System.Activities.NativeActivity.Cancel%2A>\-Überschreibung einer auf <xref:System.Activities.NativeActivity> basierenden, benutzerdefinierten `ParallelForEach`\-Aktivität definiert.Wenn die Aktivität abgebrochen wird, behandelt diese Überschreibung die Abbruchlogik für die Aktivität.Dieses Codebeispiel ist Bestandteil des Beispiels unter [ParallelForEach \(nicht generisch\)](../../../docs/framework/windows-workflow-foundation/samples/non-generic-parallelforeach.md).  
  
 <!-- TODO: review snippet reference [!code-csharp[CFX_WorkflowApplicationExample#1010](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1010)]  -->  
  
 Von <xref:System.Activities.NativeActivity> abgeleitete Aktivitäten können bestimmen, ob ein Abbruch angefordert wurde, indem die <xref:System.Activities.NativeActivityContext.IsCancellationRequested%2A>\-Eigenschaft überprüft wird und sie sich selbst als abgebrochen markieren, indem die <xref:System.Activities.NativeActivityContext.MarkCanceled%2A>\-Methode aufgerufen wird.Durch Aufrufen von <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> wird eine Aktivität nicht sofort abgeschlossen.Wie üblich schließt die Laufzeit die Aktivität ab, wenn sie keine ausstehenden Aufgaben mehr aufweist; wenn jedoch <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> aufgerufen wird, ist der abschließende Zustand <xref:System.Activities.ActivityInstanceState> anstelle von <xref:System.Activities.ActivityInstanceState>.  
  
### Abbruch mithilfe von AsyncCodeActivity  
 Auf <xref:System.Activities.AsyncCodeActivity> basierende Aktivitäten können auch eine benutzerdefinierte Abbruchlogik bereitstellen, indem die <xref:System.Activities.AsyncCodeActivity.Cancel%2A>\-Methode überschrieben wird.Wenn diese Methode nicht überschrieben wird, wird keine Abbruchbehandlung ausgeführt, wenn die Aktivität abgebrochen wird.Im folgenden Beispiel ist die <xref:System.Activities.AsyncCodeActivity.Cancel%2A>\-Überschreibung einer auf <xref:System.Activities.AsyncCodeActivity> basierenden, benutzerdefinierten `ExecutePowerShell`\-Aktivität definiert.Wenn die Aktivität abgebrochen wird, wird das gewünschte Abbruchverhalten ausgeführt.Dieses Codebeispiel ist Bestandteil des Beispiels unter [Verwenden der InvokePowerShell\-Aktivität](../../../docs/framework/windows-workflow-foundation/samples/using-the-invokepowershell-activity.md).  
  
 [!code-csharp[CFX_WorkflowApplicationExample#1020](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1020)]  
  
 Von <xref:System.Activities.AsyncCodeActivity> abgeleitete Aktivitäten können bestimmen, ob ein Abbruch angefordert wurde, indem die <xref:System.Activities.AsyncCodeActivityContext.IsCancellationRequested%2A>\-Eigenschaft überprüft wird und sie sich selbst als abgebrochen markieren, indem die <xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A>\-Methode aufgerufen wird.