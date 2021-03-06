## Persistence events

As mentioned previously, Artemis has support to persistence lifecycle to update and save an Entity. This lifecycle order is managed by a **WorkFlow** class. The default workflow is:

* **firePreEntity**: The Object received from Artemis.
* **firePreEntityDataBaseType**: As the previous event, however, to a specified database, in other words, each database has a particular database.
* **firePreAPI**: The object converted to a communication layer.
* **firePostAPI**: The entity connection as a response from the database.
* **firePostEntity**: The entity model from the API low level from the firePostAPI.
* **firePostEntityDataBaseType**: As the previous event, however, to a specified database, in other words, each database has a particular database.

Tha watch this event, just need to use an @**Observes**, a form of CDI itself.

#### ColumnWorkFlow

```java
@ApplicationScoped
public class PersonEvent {

    private static final Logger LOGGER = Logger.getLogger(PersonEvent.class.getName());

    public void observer(@Observes EntityPrePersist event) {
        LOGGER.info("Event to pre persistence" + event.getValue());
    }

    public void observer(@Observes EntityColumnPrePersist event) {
        LOGGER.info("Event to pre document persistence" + event.getValue());
    }

    public void observer(@Observes ColumnEntityPrePersist event) {
        LOGGER.info("Event to pre document entity" + event.getEntity());
    }

    public void observer(@Observes ColumnEntityPostPersist event) {
        LOGGER.info("Event to post document entity" + event.getEntity());
    }

    public void observer(@Observes EntityPostPersit event) {
        LOGGER.info("Event to post persistence" + event.getValue());
    }

    public void observer(@Observes EntityColumnPostPersist event) {
        LOGGER.info("Event to post document entity" + event.getValue());
    }
}
```

#### DocumentWorkFlow

```java
@ApplicationScoped
public class PersonEvent {

    private static final Logger LOGGER = Logger.getLogger(PersonEvent.class.getName());

    public void observer(@Observes EntityPrePersist event) {
        LOGGER.info("Event to pre persistence" + event.getValue());
    }

    public void observer(@Observes EntityDocumentPrePersist event) {
        LOGGER.info("Event to pre document persistence" + event.getValue());
    }

    public void observer(@Observes DocumentEntityPrePersist event) {
        LOGGER.info("Event to pre document entity" + event.getEntity());
    }

    public void observer(@Observes DocumentEntityPostPersist event) {
        LOGGER.info("Event to post document entity" + event.getEntity());
    }

    public void observer(@Observes EntityPostPersit event) {
        LOGGER.info("Event to post persistence" + event.getValue());
    }

    public void observer(@Observes EntityDocumentPostPersist event) {
        LOGGER.info("Event to post document entity" + event.getValue());
    }
}
```

#### KeyValueWorkFlow

```java
@ApplicationScoped
public class UserEvent {

    private static final Logger LOGGER = Logger.getLogger(UserEvent.class.getName());

    public void observer(@Observes EntityPrePersist event) {
        LOGGER.info("Event to pre persistence" + event.getValue());
    }

    public void observer(@Observes EntityKeyValuePrePersist event) {
        LOGGER.info("Event to pre document persistence" + event.getValue());
    }

    public void observer(@Observes KeyValueEntityPrePersist event) {
        LOGGER.info("Event to pre document entity" + event.getEntity());
    }

    public void observer(@Observes KeyValueEntityPostPersist event) {
        LOGGER.info("Event to post document entity" + event.getEntity());
    }

    public void observer(@Observes EntityPostPersit event) {
        LOGGER.info("Event to post persistence" + event.getValue());
    }

    public void observer(@Observes EntityKeyValuePostPersist event) {
        LOGGER.info("Event to post document entity" + event.getValue());
    }

}
```



### Events to search and remove from database



Also, there are functions to query to both retrieve and remove, at the document and column API, Artemis supports, when a query to both delete and retrieve an event is fired.



```java

public class ColumnQueryEvent {

    private static final Logger LOGGER = Logger.getLogger(ColumnQueryEvent.class.getName());

    public void observer(@Observes ColumnQueryExecute event) {
        ColumnQuery query = event.getQuery();
        LOGGER.info("Event to pre persistence" + query);
    }

    public void observer(@Observes ColumnDeleteQueryExecute event) {
        ColumnDeleteQuery query = event.getQuery();
        LOGGER.info("Event to pre persistence" + query);
    }
}


public class DocumentQueryEvent {

    private static final Logger LOGGER = Logger.getLogger(DocumentQueryEvent.class.getName());

    public void observer(@Observes DocumentQueryExecute event) {
        DocumentQuery query = event.getQuery();
        LOGGER.info("Event to pre persistence" + query);
    }

    public void observer(@Observes DocumentDeleteQueryExecute event) {
        DocumentDeleteQuery query = event.getQuery();
        LOGGER.info("Event to pre persistence" + query);
    }
}

```



