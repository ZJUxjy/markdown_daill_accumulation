# QThread用法

>.h文件
```
#include <QThread>
class Pco2Blf:public QThread
{
    Q_OBJECT
public:
    explicit Pco2Blf(QThread *parent = nullptr);
    ~Pco2Blf();
    void setExeUrl(QString);
    void setPcoUrl(QString);
signals:
    void process_str(QString);
private:
    void run();
    QString m_exeUrl;
    QString m_pcoUrl;
};
```
要点：重写run()方法，public继承自QThread，构造函数有parent，整个线程运行方法放在run函数中进行。