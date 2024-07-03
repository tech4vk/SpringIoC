This is a simple Spring framework project to show how inversion of control is used.  This use IntelliJ IDEA, with JDK 21, and Maven build

git config --global user.name "Vu Khuong"
git config --global user.email "tech4vk@gmail.com"
mkdir springs
cd springs

git clone https://github.com/tech4vk/SpringIoC.git
git status
git log --graph --oneline --decorate --all
git show --all
q
git checkout -b lesson01
git branch
git status
git log --graph --oneline --decorate --all
git show --all
q
cat pom.xml

if need to remove
sudo rm /etc/apt/sources.list.d/archive_uri-https_download_oracle_com_java_21_latest_-noble.list

sudo apt-get install default-jdk
sudo apt-get install maven



git add pom.xml
git commit -m "Update pom.xml with dependencies"

git push --all
tech4vk@gmail.com
token

mkdir src
mkdir src/main
mkdir src/main/java
mkdir src/main/java/vk
mkdir src/main/java/vk/lesson
cd src/main/java/vk/lesson
vi IOTDevice.java

package vk.lesson;

public class IOTDevice {

    String device = "Air Conditioner";
    String description = "Temperature sensor";

    public String getDevice() {
        return device;
    }

    public void setDevice(String device) {
        this.device = device;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    @Override
    public String toString() {
        return "IOTDevice {" +
                "device = '" + device + "!\'" +
                ", description = '" + description + "\'" + '}';
    }
}

vi main.java
package vk.lesson;

import org.springframework.beans.factory.support.BeanDefinitionRegistry;
import org.springframework.beans.factory.support.DefaultListableBeanFactory;
import org.springframework.beans.factory.xml.XmlBeanDefinitionReader;
import org.springframework.core.io.ClassPathResource;
import org.springframework.core.io.Resource;

public class Main {

    public static void main(String[] args) {
        Resource resource = new ClassPathResource("applicationContext.xml");
        BeanDefinitionRegistry beanFactory = new DefaultListableBeanFactory();
        XmlBeanDefinitionReader beanReader = new XmlBeanDefinitionReader(beanFactory);
        beanReader.loadBeanDefinitions(resource);
        IOTDevice myDeviceBean = (IOTDevice) ((DefaultListableBeanFactory) beanFactory)
                .getBean("myIOTDeviceBean");

        System.out.println("Bean from BeanDefinitionRegistry -- " + myDeviceBean);

    }
}

cd ../../../../..
mkdir src/main/resources
cd src/main/resources

vi applicationContext.xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

    <bean id="myIOTDeviceBean" class="vk.lesson.IOTDevice" />
    <alias name="myIOTDeviceBean" alias="myBean"/>

</beans>

cd ../../..


