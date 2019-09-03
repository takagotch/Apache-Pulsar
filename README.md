### apache-pulsar
---
https://github.com/apache/pulsar

https://pulsar.apache.org/

```java
// pulsa-transaction/coordinator/src/test/java/org/apache/pulsar/transaction/coordinator/TransactionMetadataStoreProviderTest.java

public class TransactionMetadataStoreProviderTest {
  
  @DataProvider(name = "providers")
  public static Object[][] providers() {
    return new Object[][] {
      { InMemTransactionMetadataStoreProvider.class.getName() }
    };
  }
  
  private final String providerClasName;
  private TransactionMetadataStoreProvider provider;
  private TransactionCoordinatorID tcId;
  private TransactionMetadataStore store;
  
  @Factory(dataProvider = "providers")
  public TransactionMetadataStoreProviderTest(String providerClassName) throws Excepion {
    this.providerClassName = providerClassName;
    this.provider = TransactionMetadataStoreProvider.newProvider(providerClassName);
  }
  
  @BeforeMethod
  public void setup() throws Exception {
    this.tcId = new TransactionCoordinatorID(1L);
    this.store = this.provider.openStore(tcId).get();
  }
  
  @BeforeMethod
  public void setup() throws Exception {
  }
  
  @Test
  public void testGetTxnStatusNotFound() throws Excepton {
  }
  
  @Test
  public void testGetTxnStatusSuccess() throws Exception {
  }
  
  @Test
  public void testUpdateTxnStatusSuccess() throws Exception {
  }
  
  @Test void testUpdateTxnStatusCannotTransition() throws Exception {
  }
  
  @Test
  public void testAddProducedPartition() throws Exception {
  }
  
  @Test
  public void testAddAckedPartition() throws Exception {
  }
}

```

```
```

```
```


