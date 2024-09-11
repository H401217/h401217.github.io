This is the file template fot the Group of buttons instance (not confuse with regular button)
```smali
.class public Lz6/j;
.super Lx9/j;
.source "SourceFile"

#copy of a7/b
# direct methods
.method public constructor <init>(Lme/pou/app/App;Lq9/a;Lme/pou/app/AppView;Lx9/d;)V
    .locals 7

    const/4 v5, 0x1

    const v0, 0x7f11034a

    invoke-static {v0}, Lme/pou/app/App;->h1(I)Ljava/lang/String;

    move-result-object v6

    move-object v0, p0

    move-object v1, p1

    move-object v2, p2

    move-object v3, p3

    move-object v4, p4

    invoke-direct/range {v0 .. v6}, Lx9/j;-><init>(Lme/pou/app/App;Lq9/a;Lme/pou/app/AppView;Lx9/d;ZLjava/lang/String;)V

    return-void
.end method


# virtual methods
.method protected s()Ljava/util/ArrayList;
    .locals 2

    new-instance v0, Ljava/util/ArrayList;

    invoke-direct {v0}, Ljava/util/ArrayList;-><init>()V

    new-instance v1, Lz6/h;

    invoke-direct {v1, p0}, Lz6/h;-><init>(Lx9/j;)V

    invoke-virtual {v0, v1}, Ljava/util/ArrayList;->add(Ljava/lang/Object;)Z

    
    return-object v0
.end method
```