<extoc></extoc>

# Unit Test

- what kinds of tests do you know?
    - unit test (dev, component or function level, white box) *
    - integration test (see if your code can be integrated into other codes)
    - regression test (if new code breaks existing logic) *
    - smoke test
    - end-2-end test, feature test (external behavior test, black test) *
    - black/white box (white box is when you know how the functions are implemented inside)
    - performance test *
- agile 快速迭代 ci (continuous integration) + regression test

## JUnit Test

- Annotations
- Assertions
    - `assertSame(Object a, Object b)` same references

```java
public class CalTest {
    @BeforeClass
    public static void setupAll() {
    }
    
    @AfterClass
    public static void teardownAll() {
    }
    
    @Before
    public void setUp() {
    }
    
    @After
    public void tearDown() {
    }
    
    @Test
    public void test() {
        fail("Not yet implemented");
    }
    
    @Test(expected=NullPointerException.class)
    public void test2() {
        Cal c = new Cal();
        assertEquals(c.getMedian(new int{1,2,3}), 2);
    }
}

```