```typescript
async findAllUsers({ id, page }: FindAllUserInput): Promise<FindAllUserOutput> {
  const allUsers = await this.users.find({
    where: { id },
    take: 10,
    skip: (page - 1) * 10,
  });
}
```