# Decorator PHP Design Pattern

```
<?php

interface UserRepositoryInterface
{
    public function all();
}

class UserRepository implements UserRepositoryInterface
{
    protected $model = 'User';
    
    public function all()
    {
        return $this->model;
    }
}

abstract class UserDecorator implements UserRepositoryInterface
{
    protected $repository;
     
    public function __construct(UserRepositoryInterface $repository)
    {
        $this->repository = $repository;
    }
}

class UserRepositoryDecorator extends UserDecorator
{
     public function all()
     {
         return Cache::remember('all', function()) {
            return $this->repository->all();
         });
     }
}


$userRepository = new UserRepository();
$userRepositoryDecorator = new UserRepositoryDecorator($userRepository);
echo $userRepositoryDecorator->all();
