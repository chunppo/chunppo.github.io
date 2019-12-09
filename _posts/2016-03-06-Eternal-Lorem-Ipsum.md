---
layout: post
title: The Eternal Lorem Ipsum Placeholder Text Here
author: Author Name
---

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam imperdiet urna eu dolor placerat varius. Vivamus eros augue, consequat id scelerisque nec, fringilla in est. Proin pellentesque malesuada mauris, quis aliquam augue vestibulum ac. 

## The Eternal Lorem Ipsum? chunppo
-----

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam imperdiet urna eu dolor placerat varius. Vivamus eros augue, consequat id scelerisque nec, fringilla in est. Proin pellentesque malesuada mauris, quis aliquam augue vestibulum ac. Vestibulum ut feugiat nibh. Sed faucibus felis purus, sed convallis leo dictum vehicula. 

Nam maximus tempor feugiat. Mauris tristique imperdiet nulla id egestas. Proin eget lobortis magna. Duis consectetur nibh at elit viverra congue. Ut eu turpis enim. Suspendisse laoreet, diam sed consequat sodales, felis dolor accumsan justo, nec scelerisque mi sem quis dolor. Etiam ornare venenatis massa, a suscipit ex. Ut quis lectus id nibh mattis rutrum. Nunc vel cursus eros, at blandit mi. Vivamus ac posuere libero.




## Optional
<script src="https://gist.github.com/chunppo/fe3c8805b45faa4657b3075cce0cf216.js"></script>

<pre><code>
package com.example.thyme.webfluxthymeleafhttp;

import com.sun.tools.corba.se.idl.constExpr.Or;
import lombok.AllArgsConstructor;
import lombok.Data;

import java.util.Optional;

public class OptionalTest {
    public static void main(String[] args) {
        getAddressCity(null);

        Order order = new Order(1, new Member(2, new Address("city", "120001")));

        getAddressCityForOptionalForSimple(order);
    }

    // 기본적인 null체
    private static void getAddressCity(Order order) {
        if (order != null) {
            Member member = order.getMember();
            if (member != null) {
                Address address = member.getAddress();
                if (address != null) {
                    System.out.println(address.getCity());
                    return;
                }
            }
        }

        System.out.println("Default!!");
    }

    // 잘못사용한 Optional
    private static void getAddressCityForOptional(Order order) {
        Optional<Order> orderOptional = Optional.ofNullable(order);
        if (orderOptional.isPresent()) {
            Optional<Member> memberOptional = Optional.ofNullable(orderOptional.get().getMember());
            if (memberOptional.isPresent()) {
                Optional<Address> addressOptional = Optional.ofNullable(memberOptional.get().getAddress());
                if (addressOptional.isPresent()) {
                    Optional<String> cityOptional = Optional.ofNullable(addressOptional.get().getCity());
                    if (cityOptional.isPresent()) {
                        System.out.println(cityOptional.get());
                    }
                }
            }
        }

        System.out.println("Default!!");
    }

    private static void getAddressCityForOptionalForSimple(Order order) {
        String s = Optional.ofNullable(order)
                .flatMap(orderOptional -> Optional.ofNullable(orderOptional.getMember()))
                .flatMap(memberOptional -> Optional.ofNullable(memberOptional.getAddress()))
                .flatMap(addressOptional -> Optional.ofNullable(addressOptional.getCity()))
                .orElse("Default!!");

        System.out.println(s);
    }
}

@Data
@AllArgsConstructor
class Order {
    private Integer orderNo;
    private Member member;
}

@Data
@AllArgsConstructor
class Member {
    private Integer id;
    private Address address;
}

@Data
@AllArgsConstructor
class Address {
    private String city;
    private String zipCode;
}
</code></pre>

<pre><code>
package com.chunppo.reactive;

import java.lang.reflect.Array;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class StreamTest {
    public static void main(String[] args) {
        List<Person> persons =
                Arrays.asList(
                        new Person("Max", 18),
                        new Person("Peter", 23),
                        new Person("Pamela", 23),
                        new Person("David", 12));

        Map<Integer, Object> map = persons
                .stream()
                .collect(Collectors.toMap(
                        p -> p.age,
                        p -> Arrays.asList(p.name),
                        (name1, name2) -> {
                            List lst = new ArrayList();
                            lst.add(name1);
                            lst.add(name2);
                            return lst;
                        }));

        System.out.println(map);
    }
}

class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name;
    }
}

</code></pre>
