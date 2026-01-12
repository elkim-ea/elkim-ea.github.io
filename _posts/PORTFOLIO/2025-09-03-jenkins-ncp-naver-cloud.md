<!-- ---
layout: post
title: "1. Jenkins_NCP (Naver Cloud) 생성하기 "
date: 2025-09-03
categories:
  - "AWS/Naver Cloud" 
---
<img src="{{ '/assets/img/images/NaverCloud/image.png' | relative_url }}" alt="스크린샷" width="500">

위와 같은 그림으로 순서대로 만들어갈 것이다.
We will build the environment step by step as illustrated in the diagram above.

 목표(Objectives): 
 
  1) Naver Cloud 생성하기 ( Create a Naver Cloud instance )
    
  2) VPC 생성하기 ( Set up a VPC (Virtual Private Cloud) )
    
  3) Subnet 생성하기 ( Configure a Subnet )
    
  4) NCP Jenkins Server와 NCP Deploy Server 생성하기 ( Launch an NCP Jenkins Server and an NCP Deploy Server )
    

### 1. Naver Cloud 생성하기 ( Create a Naver Cloud instance )

<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-195629.png' | relative_url }}" alt="스크린샷" width="500"> 

1) 네이버 클라우드에 가입하고 콘솔에들어간다.(Sign up for Naver Cloud and log in to the console. )                                

<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-190419.png' | relative_url }}" alt="스크린샷" width="500">

1) 필요한 것은 즐겨찾기로 추가시켜놓는다.( Add frequently used services to Favorites for quick access. )         

### 2. VPC 생성하기 ( Set up a VPC (Virtual Private Cloud) )

<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-190435.png' | relative_url }}" alt="스크린샷" width="500">

1) VPC를 생성해준다. 위의 그림과 같이 10.0.0.0/16로 정해준다.( Create a VPC — set the CIDR block to 10.0.0.0/16, as shown in the diagram above. )     

### 3. Subnet 생성하기 ( Configure a Subnet )

<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-190558.png' | relative_url }}" alt="스크린샷" width="500">

1) Subnet도 생성해준다. 이 또한 10.0.1.0/24로 정해준다.( Create a Subnet — set the CIDR block to 10.0.1.0/24. )                 

### 4. ACL (방화벽) 생성하기

<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-191159.png' | relative_url }}" alt="스크린샷" width="500">    
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-191219.png' | relative_url }}" alt="스크린샷" width="500">                 
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-191229.png' | relative_url }}" alt="스크린샷" width="500">    

1) 방화벽은 자동으로 만들어 주지만 따로 우리가 만들 수 있다.( A firewall is created automatically, but we can also create one manually if needed. )     

2) Inbound와 Outbound는 각각 만들어야한다.( Inbound and Outbound rules must be configured separately. )
               
3) Inbound는 밖에서 안이다.( Inbound means traffic coming from outside to inside. )
   
4) Outbound는 안에서 밖이다.( Outbound means traffic going from inside to outside. )                               

### 5. ACG( 보안그룹) 생성하기
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-191517.png' | relative_url }}" alt="스크린샷" width="500">
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-191534.png' | relative_url }}" alt="스크린샷" width="500">       

1) ACL 생성처럼 Inbound와 Outbound를 생성하면된다.( When creating an ACL, you need to configure both Inbound and Outbound rules.)    

2) ACL과 다르게 ACG는 Inbound만 만들어도 자동으로 Outbound가 생성된다.( Unlike ACLs, ACGs automatically create Outbound rules when you configure only the Inbound rules.)                  

### 6. NCP Jenkins Server와 NCP Deploy Server 생성하기 ( Launch an NCP Jenkins Server and an NCP Deploy Server )              
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-192058.png' | relative_url }}" alt="스크린샷" width="500">
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-193338.png' | relative_url }}" alt="스크린샷" width="500">
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-193706.png' | relative_url }}" alt="스크린샷" width="500">
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-193836.png' | relative_url }}" alt="스크린샷" width="500">
<img src="{{ '/assets/img/images/NaverCloud/2025-09-03-194156.png' | relative_url }}" alt="스크린샷" width="500">                                

1) Server를 처음에 생성하고 keypair.pem을 발급 받는다. ( Create the server first and issue the keypair.pem file. )         

2) 그리고 Jenkins Server부터 만든다 비공인 IP는 위의 그림과 같이 10.0.1.101로 한다.(Set up the Jenkins Server. As shown in the diagram above, assign the private IP address 10.0.1.101. )
                                        
3) Jenkins Serveer처럼 Deploy Server를 만든다. ( Create the Deploy Server in the same way as the Jenkins Server. )
                           
4) 그리고 keypair.pme을 가지고 각각 root의 password를 발급받는다.( Use the keypair.pem file to generate the root password for each server.)                                                
                                                
----
오늘은 목표와 다르게 더 많은 것을 설치해보았다. 그림을 통해서 보고 만들어 생성해보니 이해하기 쉬웠고 내가 지금 무엇을 하고 있는지 알 수 있어서 좋았다.                                               

현재 나는 IT 학원에서 공부를 하고있다. 수업시간에 배운 것을 복습으로 하기에 어렵지 않게 오늘은 해내었다. 복습을 하다보니 더 집중력이 생겼고 천천히 이해하면서 해나아갔다.                                   

앞으로도 이렇게 수업에 했던 공부를 따로 복습할 예정이다.                             

Today, I installed more components than I had originally planned.                                           
By following the diagram to create and set things up, it became easier to understand, and I could clearly see what I was doing — which felt great.                                     

Currently, I am studying at an IT academy. Since this was a review of what I had learned in class, it wasn’t too difficult for me to complete today’s work. As I went through the review, I found myself becoming more focused and was able to understand everything step by step at a steady pace.                                     

Moving forward, I plan to continue reviewing the lessons I learn in class on my own, so that I can strengthen my understanding even further.                     
<!-- <img scr="" alt="alt text" width="500"> -->


--- -->
