from socket import *
from time import ctime
import RPi.GPIO as GPIO
import pigpio

pi = pigpio.pi()
pi.set_mode(4, pigpio.OUTPUT)
positionRight = 0
pi.set_mode(17, pigpio.OUTPUT)
positionLeft = 0
pi.set_servo_pulsewidth(4, positionRight)
pi.set_servo_pulsewidth(17, positionLeft)

ctrCmd = ['Up', 'Down', 'Right', 'Left', 'Stop']

HOST = ''
PORT = 21567
BUFSIZE = 1024
ADDR = (HOST,PORT)

tcpSerSock = socket(AF_INET, SOCK_STREAM)
tcpSerSock.bind(ADDR)
tcpSerSock.listen(5)

while True:
        print 'Waiting for connection'
        tcpCliSock,addr = tcpSerSock.accept()
        print '...connected from :', addr
        try:
                while True:
                        data = ''
                        data = tcpCliSock.recv(BUFSIZE)
                        if not data:
                                break
                            
                        if data == ctrCmd[0]:
                                positionRight = 2500
                                positionLeft = 500
                                pi.set_servo_pulsewidth(4, positionRight)
                                pi.set_servo_pulsewidth(17, positionLeft)
                                print 'Forward'
                                
                        if data == ctrCmd[1]:
                                positionRight = 1000
                                positionLeft = 2000
                                pi.set_servo_pulsewidth(4, positionRight)
                                pi.set_servo_pulsewidth(17, positionLeft)
                                print 'Reverse'
                                
                        if data == ctrCmd[2]:
                                positionRight = 1700
                                positionLeft = 1400
                                pi.set_servo_pulsewidth(4, positionRight)
                                pi.set_servo_pulsewidth(17, positionLeft)
                                print 'Right'
                                
                        if data == ctrCmd[3]:
                                positionRight = 1600
                                positionLeft = 1250
                                pi.set_servo_pulsewidth(4, positionRight)
                                pi.set_servo_pulsewidth(17, positionLeft)
                                print 'Left'
                                
                        if data == ctrCmd[4]:
                                positionRight = 0
                                positionLeft = 0
                                pi.set_servo_pulsewidth(4, positionRight)
                                pi.set_servo_pulsewidth(17, positionLeft)
                                print 'Stop'
                        
        except KeyboardInterrupt:
                pi.stop()
                GPIO.cleanup()
tcpSerSock.close();
