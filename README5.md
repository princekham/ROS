<H4>50.Writing ROS2 Python Service Server</H4>

- ros2 interface show example_interfaces/srv/AddTwoInts
- It will show as follow
```
v/AddTwoInts
int64 a
int64 b
---
int64 sum
```
- here the ones above the dash lines are request and below is the response
- goto ->ros2_ws/src/my_py_pkg/my_py_pkg
- create a file -> touch add_two_ints_server
- add "add_two_ints_server=my_py_pkg.add_two_ints_server:main" to the setup.py in the console scripts as in

```
from setuptools import setup

package_name = 'my_py_pkg'

setup(
    name=package_name,
    version='0.0.0',
    packages=[package_name],
    data_files=[
        ('share/ament_index/resource_index/packages',
            ['resource/' + package_name]),
        ('share/' + package_name, ['package.xml']),
    ],
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='tgi-lab',
    maintainer_email='tgi-lab@todo.todo',
    description='TODO: Package description',
    license='TODO: License declaration',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            "py_node = my_py_pkg.my_first_node:main",
            "add_two_ints_server=my_py_pkg.add_two_ints_server:main"
        ],
    },
)
```
