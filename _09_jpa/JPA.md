## JPA 
## EntityManagerFactory : 영속 단위 기준으로 초기화
```java
class Java{
    public static main(String[] args){
        // EntityManager 생성
        EntityManager entityManager = Persistence.createEntityManagerFactory("jpabegin");
        // EntityTransaction 구함
        EntityTransaction transaction = entityManager.getTransaction();
        try {
            transaction.begin(); //트랜잭션 시작
            transaction.commit(); //트랜잭션 커밋
        }catch (Exception e){
            transaction.rollback(); //트랜잭션 롤백
        }finally {
            entityManager.close(); //트랜잭션 닫음
        }
    }
}
```
## 영속 컨텍스트(Persistence context)
* EntityManager 단위로 영속 컨텍스트 관리
* 커밋 시점에 영속 컨텍스트의 변경 내열을 DB에 반영
### 저장과 쿼리 실행 시점
```text
transaction.begin();
User user = new User("a@gmail.com","user",LocalDateTime.now());
entityManager.persist(user);
logger.info("EntityManager.persist 호출함");
transaction.commit(); //이 시점에서 insert 쿼리 실행
logger.info("EntityTransaction.commit 호출함");
```
### 수정과 쿼리 실행 시점
```text
transaction.begin();
User user = new User("a@gmail.com","user",LocalDateTime.now());
if(user==null){
    System.out.println("user 없음");
}else{
    String newName = "이름"+(System.currentTimeMillis()%100);
    user.changeName(newName);
    logger.info("User.changeName 호출함");
}
transaction.commit(); //이 시점에서 수정 쿼리 실행
logger.info("EntityTransaction.commit 호출함");
```

## Entity 단위 CRUD 처리
* em.persist(객체)
* em.find(class<T> entityClass, Object primaryKey)
* em.remove(객체)
  * find로 읽어온 메서드를 전달
  * 삭제 대상이 존재하지 않으면, exception 발생
* em.merge()

## Entity Mapping
* `@Entity` : 엔티티 클래스에 설정, 필수
  * 인자 없는 기본 생성자(public/protected) 필요
  * 최상위 클래스여야 함
  * final이면 안됨
* `@Table` : 매핑할 테이블 지정
* `@Id` : 식별자 속성에 설정, 필수
* `@Column` : 매핑할 칼럼명 지정
  * 지정하지 않으면, 필드명/프로퍼티명 사용
* `@Enumerated` : enum 타입 매핑할 때 설정
  * `EnumType.STRING` : enum 타입 값 이름을 저장 (문자열 타입)
  * `EnumType.ORDINAL` : enum 타입 값의 순서를 저장 (숫자 타입)

## [엔티티 식별자 생성 방식](https://www.inflearn.com/course/jpa-spring-data-%EA%B8%B0%EC%B4%88/unit/126079)