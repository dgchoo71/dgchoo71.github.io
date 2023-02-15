{
 "cells": [
  {
   "cell_type": "markdown",
   "source": [
    "[15분 안에 알아보는 파이썬 데코레이터](https://www.youtube.com/watch?v=r7Dtus7N4pI)"
   ],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%% md\n"
    }
   }
  },
  {
   "cell_type": "markdown",
   "source": [
    "# 매개변수를 데코레이터에 전달"
   ],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%% md\n"
    }
   }
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Started\n",
      "19\n",
      "Ended\n",
      "None\n",
      "==========\n",
      "Started\n",
      "Ended\n",
      "9\n"
     ]
    }
   ],
   "source": [
    "# decorator 정의\n",
    "def f1(func):\n",
    "    def wrapper(*args, **kwargs):\n",
    "        print(\"Started\")\n",
    "        val = func(*args, **kwargs)\n",
    "        print(\"Ended\")\n",
    "        return val\n",
    "\n",
    "    return wrapper\n",
    "\n",
    "# decorator 를 이용한 함수 정의\n",
    "@f1\n",
    "def f(a, b=9):\n",
    "    print(a + b)\n",
    "\n",
    "@f1\n",
    "def add(x, y):\n",
    "    return x + y\n",
    "\n",
    "print(f(10))\n",
    "print('=' * 10)\n",
    "print(add(4, 5))"
   ],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%%\n"
    }
   }
  },
  {
   "cell_type": "markdown",
   "source": [
    "# 데코레이터를 활용한 실행 시간 측정"
   ],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%% md\n"
    }
   }
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Function took: 2.01 seconds.\n"
     ]
    }
   ],
   "source": [
    "import time\n",
    "\n",
    "# decorator 정의\n",
    "def timer(func):\n",
    "    def wrapper():\n",
    "        before = time.time()\n",
    "        func()\n",
    "        print(f'Function took: {time.time() - before:.2f} seconds.')\n",
    "\n",
    "    return wrapper\n",
    "\n",
    "# decorator 를 이용한 함수 정의\n",
    "@timer\n",
    "def run():\n",
    "    time.sleep(2)\n",
    "\n",
    "\n",
    "# 함수 호출\n",
    "run()"
   ],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%%\n"
    }
   }
  },
  {
   "cell_type": "markdown",
   "source": [
    "# 데코레이터를 이용한 로그 출력"
   ],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%% md\n"
    }
   }
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "13\n"
     ]
    }
   ],
   "source": [
    "import datetime\n",
    "\n",
    "def log(func):\n",
    "    def wrapper(*args, **kwargs):\n",
    "        with open('logs.txt', 'a') as file:\n",
    "            file.write(\"Called function with \" + \" \".join([str(arg) for arg in args]) + \" at \" + str(datetime.datetime.now()) + \"\\n\")\n",
    "\n",
    "        val = func(*args, **kwargs)\n",
    "        return val\n",
    "\n",
    "    return wrapper\n",
    "\n",
    "@log\n",
    "def run(a, b, c = 9):\n",
    "    print(a + b + c)\n",
    "\n",
    "run(1, 3, c=9)"
   ],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%%\n"
    }
   }
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "outputs": [],
   "source": [],
   "metadata": {
    "collapsed": false,
    "pycharm": {
     "name": "#%%\n"
    }
   }
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 2
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython2",
   "version": "2.7.6"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 0
}