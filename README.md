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
````


1) The adapter adapter pattern changes the interface but does not change the implementation.
2) The proxy pattern changes the implementation but does not change the interface.
3) The decorator pattern changes the implementation but does not change the interface.
4) The facade pattern is a high-level level abstraction over low-level components, where the interface is changed.
