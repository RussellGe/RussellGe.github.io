---
title: Django Model
date: 2020-05-20 20:20:29
tags: Django
---
# Django Model
**每次修改models.py之后:**</br>
**python manage.py makemigrations**</br>
**python migrate**</br>
*测试版本Django == 1.10*

* 语法:</br>
class PostModel(models.Model): **命名法：词头大写**</br>
	id = models.IntergerField(primary_key = True)**将会自动增加**</br>
	
	pass
*  Filed options
</br>null: Means value can be null(use null to represent empty)
</br></br>blank: Means the value can be nonexsit 
</br></br>defult: set a defult value
</br></br>max_length: set a max length
</br></br>verbose _ name: 设置在admin中看到的名字
</br></br>choices:{ </br>**tuple格式**</br>
第一步：设置tuple对（a,b） **b为属性名，a为属性值**
</br>第二步： 在属性中加入choice = tuple的名字
</br>第三步：调用->self.b 得到所有拥有属性b的objects
</br>}
</br></br>unique: 确认唯一
</br></br>validators: 许多校验方法， validators = [validatorFunction] **validatorFunction是我们自己写的函数 需要from django.core.exceptions import ValidationError来处理出错的情况**
</br></br>error_ messages = {'keys':'values'}
</br>**keys can be: null, blank, invalid, invalid_choice, unique, and unique_for_date **
</br></br>help_ text='the help text'报错下面的提示文本
* Filed types</br>
### AutoField
##### class AutoField(**options)
An IntegerField that automatically increments according to available IDs. You usually won’t need to use this directly; a primary key field will automatically be added to your model if you don’t specify otherwise. See Automatic primary key fields.
### BigAutoField
#### class BigAutoField(**options)
A 64-bit integer, much like an AutoField except that it is guaranteed to fit numbers from 1 to 9223372036854775807.
### BinaryField
#### class BinaryField(max_length=None, **options)
A field to store raw binary data. It can be assigned bytes, bytearray, or memoryview.
</br>
By default, BinaryField sets editable to False, in which case it can’t be included in a ModelForm.
</br>
BinaryField has one extra optional argument:
1.   BinaryField.max_length</br>
The maximum length (in characters) of the field. The maximum length is enforced in Django’s validation using MaxLengthValidator.
### BooleanField
#### class BooleanField(**options)
A true/false field.
</br>
The default form widget for this field is CheckboxInput, or NullBooleanSelect if null=True.  (当null = True：3重表达， True；False；Null)
</br></br>
The default value of BooleanField is None when Field.default isn’t defined.
### CharField
#### class CharField(max_length=None, **options)
A string field, for small- to large-sized strings.
</br></br>
For large amounts of text, use TextField.
</br></br>
The default form widget for this field is a TextInput.
</br></br>
CharField has one extra required argument:
</br></br>
CharField.max_length
The maximum length (in characters) of the field. The max_length is enforced at the database level and in Django’s validation using MaxLengthValidator.
### SlugField
#### class SlugField(max_length=50, **options)
Slug is a newspaper term. A slug is a short label for something, containing only letters, numbers, underscores or hyphens. They’re generally used in URLs.
</br></br>
Like a CharField, you can specify max_length (read the note about database portability and max_length in that section, too). If max_length is not specified, Django will use a default length of 50.
</br></br>
Implies setting Field.db_index to True.
</br></br>
It is often useful to automatically prepopulate a SlugField based on the value of some other value. You can do this automatically in the admin using prepopulated_fields.
</br></br>
It uses validate_slug or validate_unicode_slug for validation.
</br></br>
SlugField.allow_unicode¶
If True, the field accepts Unicode letters in addition to ASCII letters. Defaults to False.
### SmallAutoField
#### class SmallAutoField(**options)
Like an AutoField, but only allows values under a certain (database-dependent) limit. Values from 1 to 32767 are safe in all databases supported by Django.
### DateField
#### class DateField(auto_now=False, auto_now_add=False, **options)
A date, represented in Python by a datetime.date instance. Has a few extra, optional arguments:

DateField.auto_now¶
Automatically set the field to now every time the object is saved. Useful for “last-modified” timestamps. Note that the current date is always used; it’s not just a default value that you can override.

The field is only automatically updated when calling Model.save(). The field isn’t updated when making updates to other fields in other ways such as QuerySet.update(), though you can specify a custom value for the field in an update like that.

DateField.auto_now_add¶
Automatically set the field to now when the object is first created. Useful for creation of timestamps. Note that the current date is always used; it’s not just a default value that you can override. So even if you set a value for this field when creating the object, it will be ignored. If you want to be able to modify this field, set the following instead of auto_now_add=True:

For DateField: default=date.today - from datetime.date.today()
For DateTimeField: default=timezone.now - from django.utils.timezone.now()
The default form widget for this field is a DateInput. The admin adds a JavaScript calendar, and a shortcut for “Today”. Includes an additional invalid_date error message key.

The options auto_now_add, auto_now, and default are mutually exclusive. Any combination of these options will result in an error.
*  Meta与其他</br>
可设置verbose_name _plural 显示在admin中的，表示多个objects的名字</br>
unique_together = [('一个Field','另一个Field')] **让两个Field一起的值unique**</br>
非Meta但是一起记了：
</br>def  __ str __(self):
</br>return smart _text (self.title) 返回一个新的名字（admin里可见，替换post）</br>
**python2里是unicode/smart _text让它能自适应语言**
</br>slugnify()让名字中间空格变为-并且unique，自动添加重复名后计数
</br>overwriting save：</br>
def save(self, * args, * kwargs) **可以overwriting用来设置一些有依赖的值的自动构建，比如slug可以用slugnify(self.title)来完成**
</br>发布了多久</br>**from django.utils.timesince import timesince**
</br>**用timesince(某事件)得到过了多久**
##  ModelManagers
**class PostModelManager(models.Manager):
		def all(self, * args, ** kwargs):可以让flag等于False的不显示**
## signals
**用于在models储存或删除时传递信息**
**django.db.models.signals.pre _save & django.db.models.signals.post _save**</br>

* 用法:</br>
def preSaveReciver(sender, instance, created, * args, ** kwargs):**可以用pre_ save.connect(preSaveReciver, sender = PostModel) 来接收**
pre_save()
</br>
　　　　django.db.models.signals.pre_save
</br>
　　　　在model执行save方法前被调用
</br>
　　　　5个参数：
</br>
　　　　　　pre_save（sender，instance，raw，using，update_fields）
</br>
　　　　　　　　sender：model类
</br>
　　　　　　　　instance：保存的实例
</br>
　　　　　　　　raw：一个Boolean类型，如果model被全部保存则为True
</br>
　　　　　　　　using：使用的数据库别名
</br>
　　　　　　　　update_fields：传递的待更新的字段集合，如果没有传递，则为None
</br>
　　post_save()
</br>
　　　　djang.db.models.post_save
</br>
　　　　在model执行完save方法后被调用
</br>
　　　　6个参数
</br>
　　　　　　post_save（sender，instance，created，raw，using，update_fields）
</br>
　　　　　　　　sender：model class
</br>
　　　　　　　　instance：被保存的model实例
</br>
　　　　　　　　created：Boolean值，如果创建了一个新的记录则为True
</br>
　　　　　　　　raw：Boolean值，如果model被全部保存则为True
</br>
　　　　　　　　using：使用的数据库别名
</br>
　　　　　　　　update_fields：传递的待更新的字段集合，如果没有传递，则为None
</br>
　　pre_delete()
</br>
　　　　django.db.models.signals.pre_delete
</br>
　　　　在执行model的delete（）或者queryset的delete（）方法前调用
</br>
　　　　pre_delete(sender,instance,using)
</br>
　　　　　　sender：model class
</br>
　　　　　　instance：被删除的实例
</br>
　　　　　　using：使用的数据库别名
</br>
　　6）post_delete（）
</br>
　　　　django.db.models.signals.post_delete
</br>
　　　　在执行model的delete（）或者queryset的delete（）方法后调用
</br>
　　　　post_delete(sender, instance，using)
</br>
　　　　　　sender：model class
</br>
　　　　　　instance：被删除的实例，注意：此时，该实例已经被删除了，数据库中不再有这条记录，所以在使用这个实例的时候要格外注意
</br>
　　　　　　using：被使用的数据库别名
	

