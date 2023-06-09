# Scenarios

## Adding a report


```mermaid

sequenceDiagram
    Reporter->>UI: LogIn
    UI->>Reporter: Response
    UI->>ClientsAPI: Fetch project & client data
    ClientsAPI->>UI: 
    Reporter->>UI: CreateReport()
    UI->>ReportAPI: FetchData()
    ReportAPI->>UI: Response Data
    UI->>Reporter: Form Data
    Reporter->>UI: SubmitForm()
    UI->>ReportAPI: PostData()
    ReportAPI->>ReportAPI: StoreReport
    ReportAPI->>MessagingPlatform: RaiseReportAddedEvent
    ReportAPI->>UI: 
    UI->>Reporter: 
        MessagingPlatform->>OrchestrationService: ReceivedReportAddedEvent()
    alt RAGStatusRed
    OrchestrationService->>UserService: WhoWantsThisReport()
    UserService->>OrchestrationService: 
    OrchestrationService->>MessagingPlatform: SendNotification()    
    MessagingPlatform->>NotificationService: ReceivedSendNotification
    NotificationService->>EmailService: SendAnEmail()

    end    

    
```
