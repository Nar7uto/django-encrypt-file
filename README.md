### Django File Encrypt

This package can be used to encrypt Django's in memory files to encrypt them.

## Basic Usage:

    from django_encrypt_file import EncryptionService
    from django.core.files import File

    password = '1234'
    service = EncryptionService(raise_exception=False)

    open('readme.md', 'rb') as inputfile:
        usefile = File(inputfile, name='readme.md')
        encrypted_file = service.encrypt_file(useFile, password, extension='.enc')  # it will save readme.md.enc
        decrypt_file = service.decrypt_file(encrypted_file.name, password, extension='.enc') # it will remove .enc extension

### Using in Views:

    from django_encrypt_file import EncryptionService, ValidationError


    def some_view(request):
       try:
           myfile = request.FILES.get('myfile', None)
           password = request.POST.get('password', None
           encrypted_file = EncryptionService().encrypt_file(myfile, password, extension='.enc')
           decrypt_file = service.decrypt_file(encrypted_file.name, password, extension='.enc') # it will remove .enc extension
       except ValidationError as e:
           print(e)

Input file here can be any kind of Django File Object like `models.FileField` or `forms.FileFiled`.
extension is optional if you want to store your encrypted files in another extension.
raise_exception will throw `ValidationError` error which can be imported `from django_encrypt_file import ValidationError`

