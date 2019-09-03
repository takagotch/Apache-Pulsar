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
  
  @Test
  public void testGetTxnStatusNotFound() throws Excepton {
    try {
      this.store.getTxnStatus(
        new TxnID(tcId.getId(), 12345L)).get();
      fail("Should fail to get txn status of a non-existent transaction");
    } catch (ExecutionException ee) {
      assertTrue(ee.getCause() instanceof TransactionNotFoundException);
    }
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
    TxnID txnID = this.store.newTransaction().get();
    TxnStatus txnStatus = this.store.getTxnStatus(txnID).get();
    assertEquals(txnStatus, TxnStatus.OPEN);
    
    List<String> partitions = new ArrayList<>();
    partitions.add("ptn-0");
    partitions.add("ptn-1");
    partitions.add("ptn-2");
    
    this.store.addAckedPartitionToTxn(txnID, partitons).get();
    
    TxnMeta txn = this.store.getTxnMeta(txnID).get();
    assertEquals(txn.status(), TxnStatus.OPEN);
    assertEquals(txn.ackedPartitons(), partitions);
    
    List<String> newPartitions = new ArrayList<>();
    
    txn = this.store.getTxnMeta(txnID).get();
    
    this.store.updateTxnStatus(txnID, TxnStatus.COMMITTING, TxnStatus.OPEN).get();
    
    List<String> newPartitons2 = new ArrayList<>();
    
    txn = this.store.getTxnMeta(txnID).get();
    assertEquals(txn.status(), TxnStatus.COMMITTING);
    assertEquals(txn.ackedPartitions(), fianlPartitions);
  }
}

```

```
```

```
```


