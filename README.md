# 学习php的知识

## 一、设计模式学习

### 1.单例模式
        
        <?php
        /*
        *单例模式
        */
        class Database{
               //四个私，一个公
               //用于保存当前实例化后的对象
               private static $instance = null;
               //数据库连接句柄
               private $db = null;
               //构造方法声明为私有方法,静止外部使用
               private function __construct($config =array())
               {
                     $dsn = sprintf('mysql:host=%s;dbname=%s',$config["db_host"],$config["db_name"]);
                     $this->db = new PDO($dsn,$config["db_user"],$config["db_pwd"]);
               }
               //获取当前容器的实例(单例)
               public static function getInstance($config=array()) 
               {
                     if(self::$instance == null||is_null(self::$instance)){
                        self::$instance = new self($config);
                     }
                     return self::$instance;
               }
               //获取数据库句柄
               public function db(){
                      return $this->db();
               }
               //声明私有方法禁止克隆，禁止重建对象
               private function __clone(){};
               private function __wakeup(){};
        }
        $config = array(
                "db_name"=>'php_test',
                "db_host"=>'localhost',
                "db_user"=>'root',
                "db_pwd"=>''
                );
        
        
