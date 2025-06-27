附件中我上传了两版本代码，2nd（对话接口 Chat API）与3rd（补全接口 Completion API）。 要让脚本通过API达到想要的效果，需要尝试多种不同的接口：批量生成较适合使用补全，总结类较适合ChatAPI。因为需要让模型逐行处理数据生成summary，目前我觉对话接口稍好一点。
对话接口方法：client.chat.completions.create(...) 用法：使用messages,role,content等输入，维护一段结构化对话，它按照角色接着回复
补全接口方法：client.completions.create(...) 用法：给模型一个长prompt后，他来续写。缺点是上下文要全部手动拼接。 补全需要将所有角色设定都写到prompt里。对话中则需写在role中，system设定“角色设定”，user提问
<img width="934" alt="image" src="https://github.com/user-attachments/assets/e55682c3-9b2c-4932-bcac-1ef1513ea0ed" />
<img width="699" alt="image" src="https://github.com/user-attachments/assets/a803e0f8-8e4e-4b8a-9c19-a20c0e9c6bc6" />
2nd(对话接口)脚本中，可以直接把问题写成一段完整的文字: *"Based only on information before October 2023, summarize Mayo Clinic's AI adoption timeline."* 然后把它传给模型生成结果。这种方式比较直接，模型会把它当作“文章开头”来续写。适合一些模板化的问题。缺点是最终输出的内容格式不太稳定，较为死板，有时候会答偏。
![image](https://github.com/user-attachments/assets/8c33a23d-4ac9-4da8-b337-d5974d5c1bb7)
3rd补全接口会直接生成一大段，能更好地理解提问，因为代码中描述的多。很容易受prompt影响，稍有改动可能输出就会答非所问或者相差很多，目前效果最好的就是补全。
![image](https://github.com/user-attachments/assets/5066f91c-7863-4831-ba30-28986922936f)
<img width="550" alt="image" src="https://github.com/user-attachments/assets/f08b00a9-130b-414d-8be0-42deb0c3fad4" />
