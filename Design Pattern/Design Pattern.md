# DesignPattern 

---  
### 목차  
* [빌더패턴](#빌더패턴)
---  

## 빌더패턴
 클래스 변수가 많을 경우, 클래스 변수가 선택사항이 있는 경우등, 생성자의 숫자가 늘어나거나 매개변수가 많아진다.

```java
public class Pet{
    private final Animal animal;
    private final String petName;
    private final String ownerName;
    private final String address;
    private final String telephone;
    private final Date dateOfBirth; // 선택사항 1
    private final String emailAddress; // 선택사항 2
}
```
위와 같은 데이터 클래스가 있다고 가정한다면, 매개변수는 5~7개 필요하고, 선택사항이 없는 경우, 선택사항 1만 있는 경우, 선택사항 2만있는 경우, 선택사항 1,2를 모두 포함하는 경우 모두 4가지의 생성자가 필요하다.  
한가지 방법은 생성자를 사용하지 않고 getter와 setter를 사용하는 방법이다. 하지만 필수 항목을 설정하지 않아 유요하지 않은 객체를 생성할 수도 있다.  
  
  이와 같은 상황에서 빌더패턴을 사용해보자.
```java
public class Pet{
    public static class Builder{ // 객체안에 빌더 클래스를 정의한다.
        private Animal animal = new Dog(); // 미리 기본값을 지정할 수도 있다.
        private String petName;
        private String ownerName;
        private String address;
        private String telephone;
        private Date DateOfBirth;
        private String emailAddress;
        
        public Builder withAnimal(final Animal animal){
            this.animal = animal;
            return this;  // 객체자신을 리턴한다.
        }
        
        public Builder withPetName(final String petName){
            this.petName = petName;
            return this; 
        }
        
        public Builder withOwnerName(final String ownerName){
            this.ownerName = ownerName;
            return this;
        }
        
        ...
        
        public Builder withEmailAddress(final String eamilAddress){
            this.emailAddress = eamilAddress;
            return this;
        }
        
        public Pet build(){
            if(animal == null || petName == null || ... address == null){ // 선택사항은 유효성겁사를 하지 않는다.
                throw new IllegalStateException("Cannot create Pet"); 
            }
            return new Pet(
                    animal,
                    petName,
                    ownerName,
                    address,
                    telephone,
                    dateOfBirth
                    emailAddress);
        }
    }
    
    private final Anmail animal;
    private final String petName;
    private final String ownerName;
    private final String address;
    private final Date dateOfBirth; // 선택사항
    private final String emailAddress; //선택사항
    
    private Pet(final Animal animal,  // 생성자의 접근자를 private으로 지정하여 Builder 에서만 접근할 수 있도록 한다.
            final String petName,
            ...
            final String emailAddress)
        this.animal = animal;
        ...
        this.emailAddress = emailAddress;
        
        }
}
```
